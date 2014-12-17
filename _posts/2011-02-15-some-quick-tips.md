---
author: Aishwarya Singhal
comments: true
date: 2011-02-15 03:55:16+00:00
layout: post
slug: some-quick-tips
title: Some Quick Tips
wordpress_id: 52
tags:
- Rails
- Ruby
---

1. Removing a column from a table in SQLite

	There's no straight forward way in SQLite so you need to copy the contents into a new table drop and recreate the table and put the data back in. In short, its a big mess. Thankfully rails manages that for us.

	```ruby
		rails generate migration RemoveUserIdFromProjects user_id:integer
		rake db:migrate
	```

2. Creating static data

	I needed some static data in my application, specifically project statuses, but I wanted to have an ability to maintain them in the database so we could add/ remove them as needed. The way I did it was through Fixtures. All you need to do is:

	a. Inside the db/migrate directory, create a directory called init_data. Create a file called `<tablename>.yml` inside init_data. Copy the format from model yml inside the test directory of the project. Oh by the way, you would need to have a model for the table, obviously.

	b. Create a file called `<a number>_load_<table name>.rb` inside db/migrate. Adjust the number so that the file appears at the end of the directory listing by name. The following is what I created for my model (called State). I guess you can use it as is - just find and replace State with your model name :-)

	```ruby

		require 'active_record/fixtures'
		class LoadStates < ActiveRecord::Migration

		def self.up

		down()
		 directory = File.join(File.dirname(__FILE__), "init_data")

		Fixtures.create_fixtures(directory, "states")

		end

		def self.down

		State.delete_all

		end

		end

	```

	Thats it - now run rake db:migrate and it will load all data as defined in the fixture YML.
	
3. Adding a URL to an existing controller

	e.g. I needed to add a URL /projects/load to call method `load()` in my projects controller. Add the following in routes.rb before the resource definition:

	```ruby

	match 'projects/load' => 'projects#load'

	```
