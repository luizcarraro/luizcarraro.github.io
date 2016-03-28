---
layout: post
title: An automatic mongodb backup aproach
excerpt_separator: <!--more-->
---

So today I was setting up one of the servers for creating automatic backups from time to time and uploading it to an amazon S3 and I tought I should share some of it here. Therefore, I'll talk about automatic backup in a folder. Some other time I'll talk about s3 upload from linux shell.

So first of all, you should create an script for some standard mongodb operations. Mine will be called automatic-mongo-backup.sh

~~~
$ touch automatic-mongo-backup.sh
~~~

Then with your favorit text editor you can place the following inside the file:

{% highlight sh linenos %}
mongodump --db=<database-name>
DATE=$(date "+%Y-%m-%d-%H-%M-%S")
tar -cvzf ./dump/$DATE.tar.gz ./dump/<database-name>
rm -rf ./dump/
{% endhighlight %}


The first line created the database dump at the same folder the script is being executed. 
Line two gets todays date and then line tree will compact the folder with tar command and the name will be the current date and time. 

Line four will then remove the dump folder.




By now, everytime you execute ```automatic-mongo-backup.sh``` you will generate a compacted dump with the moment date and time. But we need it to be automatic and with no need for us to access the server. So we're going to use ubuntu's default cron manager.

you shuould first set your priorities time for your cron, one simple way is to use http://crontab-generator.org/

Mine should backup the database every day at midnight so it looked just like this:

~~~
0 0 * * * /home/ubuntu/automatic-mongo-backup.sh  >/dev/null 2>&1
~~~

You must now add it to the cron's file by runing

~~~
$ crontab -e
~~~

Where you may be prompted to select an editor.

Now if everything is fine, you should hit ```$ service cron restart``` and be happy.

See ya fellas!
