---
layout: post
title: "Quick Guide to Shelf Management with calibre 0.9.1 & above (Touch / Glo / Mini /Aura)"
date: 2013-10-26 15:45:00 +0000
comments: true
categories:
published: false
---
Source [http://www.mobileread.com/forums/showthread.php?t=193184](http://www.mobileread.com/forums/showthread.php?t=193184)

- - -

With the new Kobo driver introduced with calibre 0.9.1, there has been some confusion over how to automate the management of shelves.

The steps I use are the following

### Driver / calibre Configuration

1. Added a custom column to calibre
	* Preferences | Change Calibre Behaviour | Add your own columns
	* Select Add custom column
	* Select Tags in Quick create
	* I used *Lookup Name* myshelves and *Column heading* My Shelves
	* Do make sure this column is of type Comma separated text, like tags, shown in the tag browser
2. Configured either the Kobo Touch or the Kobo Touch Extended driver depending on which you are using.
	* Preferences | Advanced | Plugins
	* Expand Device Interface plugins section and look for KoboTouch or Kobo Touch Extendeddriver
	* With KoboTouch or Kobo Touch Extended highlighted, select Customize plugin
	* In the area for shelf info, type #myshelves, series.  
	(Any time a custom column is used within calibre, it HAS to be referenced with a # symbol in front of it.)
	* Select any other relevant options. It is suggested that at a minimum you select the Create Bookshelves and Delete Empty Bookshelves options. The other options are not shelf specific.

Now, when you edit the metadata for a book, look for the Custom Metadata area (where it is found depends on the view you are using). In the field My Shelves type in whatever shelves you want the books to be placed.

If you do as I did and also add series to the driver options, a shelf will be created automatically for each book series, and the books added to that shelf.

### Configuring calibre's Metadata Management options

Calibre has three options as to when it updates Metadata on the device. This also affects when the shelves are managed on the Kobo.

This option is managed as follows:

* Preferences | Import/Export | Sending books to devices
* The Metadata management selection has three options
	* Manual management: Calibre updates the metadata and adds collections only when a book is sent. With this option, calibre will never remove a collection.
	* Only on send: Calibre updates metadata and adds/removes collections for a book only when it is sent to the device.
	* Automatic management: Calibre automatically keeps metadata on the device in sync with the calibre library, on every connect
* As can be seen from the descriptions, for full functionality of the Kobo driver, set the Metadata management to either Only on send or Automatic management. From my experience, I have seen the easiest option to be Automatic management.If the option is set to Manual management, shelves will NEVER be removed.

### Changing Book Titles to include Series Info

One probably also wants to change book titles to include Series info. That gets done via what is called a "metadata plugboard". Through these you are able to modify items like the book's title or author as it gets transferred to your device.

Goto Preferences | Import/Export | Metaboard plugboards

It looks complex, but is not.

On the line that reads Add new plugboard do the following

* In the box Format (choose first) select epub
* In the Device (choose second) box select KOBOTOUCH
* In the Source Template the magic happens. Here you have a lot of options
	* To modify the book's title to &lt;Series&gt; - &lt;Number&gt; - &lt;Title&gt; type. Code:

			{series}{series_index:0>2s| - | - }{title}

	* To modify the book's title to &lt;Number&gt; - &lt;Title&gt; type. Code:

			{series_index:0>2s|| - }{title}
	* To modify the book's title to &lt;First Letter of Each word in Series&gt; - &lt;Number&gt; - &lt;Title&gt; type. Code:

			{series:re(([^\s])[^\s]+(\s|$),\1)}{series_index:0>2s| - | - }{title}

* Finally in Destination Field select title

Once all that is done, take a DEEP breath and hit the Save Plugboard button and then the Apply checkmark at the top of the screen.