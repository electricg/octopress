---
layout: post
title: "How to install WordPress with ssh"
date: 2012-10-22 20:10:00 +0000
comments: true
categories:	
---
To avoid a waste of time downloading, unzipping and uploading the WordPress files, I used this method to install it through ssh on my 1&1 hosting (the *$* symbol is just to show that it's a console command, there's no need to digit it):

1. Connect to your server via ssh

		ssh yourusername@yourserver

2. Insert password when requested

3. Once connected, download the latest version of [WordPress](http://wordpress.org/)

		$ wget http://wordpress.org/latest.tar.gz

4. Unarchive the downloaded file, where the parameter x is for extract, z is for the gzip format used and f is to specify from which file

		$ tar -zxf lastest.tar.gz

5. Rename the created wordpress folder to the desired one

		$ mv wordpress/ blog/

6. Follow the [Famous 5-Minute Install](http://codex.wordpress.org/Installing_WordPress#Famous_5-Minute_Install) skipping point 1 and 5, while for the point 3 and 4 work directly on the server. The file can be renamed through ssh

		$ mv wp-config-sample.php wp-config.php
and edited using any console editor the server has installed, such as nano or vim.