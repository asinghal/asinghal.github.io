---
author: Aishwarya Singhal
comments: true
date: 2011-02-15 03:59:26+00:00
layout: post
slug: reading-excel-in-rails
title: Reading Excel in Rails
wordpress_id: 57
tags:
- Rails
- Ruby
---

Whatever the search results say, you probably don't need a plugin. I had a hard time trying to make parseexcel work and it kept reading my excel file all wrong. I finally have used win32ole which comes bundled up with rails 3. Here's the source code

```ruby
xl = WIN32OLE.connect('Excel.Application')
workbook = xl.ActiveWorkbook
worksheet = workbook.Worksheets(1);
data = worksheet.UsedRange.Value
#   Grab first row of data to use as field names      
data.shift
data.each do |row|
i=0
row.each { |cell|print cell.to_s
i = i+1
}
end
```

There are two problems with this: firstly, you need to have the sheet open in excel for this to work, and secondly once you have executed this code, you will need to restart server before you can read the same file again. I am sure there's a way around both but I haven't figured it out yet :smile:
