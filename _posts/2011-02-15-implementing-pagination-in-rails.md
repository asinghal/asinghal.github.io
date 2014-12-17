---
author: Aishwarya Singhal
comments: true
date: 2011-02-15 03:37:16+00:00
layout: post
slug: implementing-pagination-in-rails
title: Implementing Pagination in Rails
wordpress_id: 48
tags:
- Rails
- Ruby
---

Implementing pagination in Rails is dead easy. I used a plug in called will_paginate. The usual one that's downloaded when you say "gem install mislav-will_paginate" didn't work for me. It kept on escaping the HTML so all I got was garbled text on the screen. The one that did work was "gem install agnostic-will_paginate".

```ruby

gem install agnostic-will_paginate

```

Once you have that, (and for some reason gems don't get auto installed for me so I need to copy the .rb file and library into ruby's directory), all you need to do is that you in your view add the following line :

```ruby

<%= raw will_paginate @projects %>

```

Notice the "raw", it tells rails not to escape the HTML.

As you may have guessed, Project is a model in my app. The next thing is to modify the lookup code (I have it in my model but you could have it in controller too). You need to just add a call to the paginate method on the ActiveRecord resultset (so append your existing lookup code with `.paginate(...)`) Nothing complex, no tweaking the existing code apart from adding this call. And it does what it says on the tin - it paginates the collection!

```ruby

page = params[:page] || 1

find(:all,  :order => 'project_key ASC').paginate(:per_page => 20, :page => page)

```

Yeah that really is it, easy isn't it? The only thing that worries me is that this pagination seems to be happening in the application, so if I have a large record set, I would be collecting all of it on all pages - sounds like of a waste of memory. I would like to do it at database level but haven't figured that out yet.
