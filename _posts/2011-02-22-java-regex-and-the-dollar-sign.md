---
author: Aishwarya Singhal
comments: true
date: 2011-02-22 18:20:18+00:00
layout: post
slug: java-regex-and-the-dollar-sign
title: Java Regex and the Dollar Sign
wordpress_id: 63
tags:
- J2EE
---

I came across an interesting problem today that got 3 hrs wasted for no good reason. In my application, I have templates and I replace variables with values that are read from a file. And I use the plain old `String.replaceAll` to do the job. So it happened this afternoon that I landed upon the following error:

	java.lang.IllegalArgumentException: Illegal group reference	
	at java.util.regex.Matcher.appendReplacement(Matcher.java:713)	
	at java.util.regex.Matcher.replaceAll(Matcher.java:813)	
	at java.lang.String.replaceAll(String.java:2189)

As informative as it is, I did a bit of debugging and read a few articles only to realise that it was a dollar sign ($) in one of the values that was causing the issue. Now the deal is that Java regex uses the $ sign as a group separator and so it does not like that to appear in the text. Suggestions on the net include escaping the $ with back slashes but no matter how many slashes I put, it did not work.  So I wrote a simple little hack:

```java
static String escapeForRegex(final String text) {
	String modifiedText = text;
	if (text.contains("$")) {
		StringBuffer sb = new StringBuffer();
		for (char c : text.toCharArray()) {
			if (c == '$') {
				sb.append("__DOLLAR_SIGN__");
			} else {
				sb.append(c);
			}
		}
		modifiedText = sb.toString();
	}

	return modifiedText;
}
```

And when you are done with all replacements on the string, just do a

```java

text.replaceAll("__DOLLAR_SIGN__", "\\$")

```

I know, its a hack. Unfortunately I haven't found a better way out yet. Posting so that if somebody needs it in desperate times, he does not have to spend 3 hrs on it.
