---
author: Aishwarya Singhal
comments: true
date: 2011-02-15 03:18:14+00:00
layout: post
slug: ruby-jquery-and-ajax
title: Ruby, JQuery and AJAX
wordpress_id: 29
categories:
- JQuery
- Ruby
---

Since my last post, I got busy with some pressing project work and Ruby on Rails took the backseat. But I picked it up again last week and, as promised, tried a "real" app. Now Ruby is all cool and stuff, but there are gotchas everywhere and I noticed a few that I thought I'll put up here.

1. Chrome, AJAX and JQuery

[This ](https://github.com/augustl/sample-rails-apps)is what I used as an example. Note that the main things are: application.js which defines all the JS functions, the RJS file which prepares the response (using partials) and the fact that the controller responds to a JS as well e.g.

```ruby

respond_to do |format|

format.html

format.js {render :layout => false}

end

```

Also, you would need to include the following line in application.html.erb

```ruby
<%= javascript_include_tag 'http://ajax.googleapis.com/ajax/libs/jquery/1.2.6/jquery.min.js', 'jquery.livequery.js', 'jquery.form.js', 'application', 'jquery.watermark.js' %>
```

Its quite easy if you are able to set it up right. Just follow the example code and you'll be fine.
Alright, the main problem I landed up with was that JQuery kept dumping raw javascript onto my screen, so things like try catch blocks with JS code popped up instead of the HTML I had expected. And it took me a frustrating 2 hours before I found an article that said it was a Chrome problem. Ah well, I was using Chrome (and still am). The issue is that Chrome doesn't like line breaks in the response coming back via AJAX. The fix is simple, in your application.js where you are getting response back, just add this line:

```javascript
response = replace(response, "\n", "");
```

That's it, it works like magic now.

2. Using watermarks

I wanted to place instructions inside my input text form fields so that I could save space on labels. The way I did it was by using a cool library called [watermarks](http://plugins.jquery.com/project/Watermark). Try it - its nice and easy. The only catch I saw (and I could be wrong myself) was that the text didn't exactly appear in the text box. The way I fixed it was by tweaking the CSS inside the jquery.watermark.js as follows:

```javascript

l.css({position:"absolute",left:"5px",display:"inline",cursor:"text"});

if(!o.el.is("textarea")) { l.css({top:($.browser.mozilla)?"-2px" : "-5px"}); };

```

These lines would already be in the code - I just tweaked the pixel numbers.
