---
author: Aishwarya Singhal
comments: true
date: 2012-05-17 16:04:08+00:00
layout: post
slug: generating-excel-in-play-2
title: Generating Excel in Play 2
wordpress_id: 109
tags:
- PlayFramework
- scala
---

Play 1.x has a nice module that allows you to create Excel sheets. The new Play 2.x however lacks this capability. Or atleast is not very evident. While I found most of the information by searching the net, I thought it may help someone to just have quick start notes here.

1. I use [Apache POI](http://poi.apache.org/spreadsheet/quick-guide.html) to generate Excel. I also wanted to create .xlsx rather than a plain .xls.

2. Add the following to your Build.scala (under APP_HOME/project)

	```scala
	val apache_poi = "org.apache.poi" % "poi" % "3.8"
	val apache_poi_ooxml = "org.apache.poi" % "poi-ooxml" % "3.8"
	val appDependencies = Seq(
	    ... apache_poi, apache_poi_ooxml
	    )
	```

Actually, you don't need ooxml if you only want to create a plain xls (and not a xlsx).

3. Now start the Play console ('play') and execute 'run'. This will resolve the dependencies and get you the requisite libraries.

4. Now generate a excel:

	```scala
	import java.io.File
	import java.io.FileOutputStream
	import org.apache.poi.xssf.usermodel._
	val file = new File("mydata.xlsx")
	val fileOut = new FileOutputStream(file);
	val wb = new XSSFWorkbook
	val sheet = wb.createSheet("Sheet1")
	var rNum = 0
	var row = sheet.createRow(rNum)
	var cNum = 0
	val cell = row.createCell(cNum)
	cell.setCellValue("My Cell Value")
	wb.write(fileOut);
	fileOut.close();
	```


5.  All done! Now, in your controller action, add the following:

	```scala
	Ok.sendFile(content = file, fileName = _ => "mydata.xlsx")
	```

