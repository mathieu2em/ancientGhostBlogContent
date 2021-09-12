---
title: Creating Periodic MySQL Backups From Scratch.
slug: creating-mysql-backups
date_published: 2020-06-25T01:10:14.000Z
date_updated: 2021-01-22T08:27:05.000Z
tags: database, Getting Started, mariaDB, bash, crontab
excerpt: friendly tutorial on how to create mysql backups on a regular basis using crontab and some bash scripting
---

Every programmer at some point makes a disaster and flush an entire database or erase some important content from things he is working on.

Then , we learn to protect ourselves!

And when we are talking about databases, well, the best way to do so is with backups !

So, after flushing my entire database doing some noobish disastrous manoeuver, I decided that maybe a periodic backup system would be a good idea. ( lol... Intelligence is learning from our mistakes right ? Or as my grandma always said "people who do nothing never fail !" :P ) 

The database I had to protect was hosted on a private server of my university; which means : NO SUDO PERMITTED. Well. Yes, but only through contact with the IT staff.

SO, I decided I would find a way to do the most I can without sudoing anything.

## The First Idea 

I did some researches and came with[ this solution ](https://medium.com/@mhagemann/how-to-backup-mysql-databases-automatically-on-ubuntu-17-10-a2b29fb47ac9)which wasnt that bad. But, as I said, I needed a NO SUDO solution. 

SO , I contacted mr Raouf , the coolest IT guy from my university which told me about cron tabs and mysqldump. He did it just like a chineese master to its apprentice, showing the way but still letting me learn and search my way through this all.
It sparkled a light in me and I began my investigation on cron tabs. 勞

### What is a CRON tab ? 

first, I had to learn about CRON tabs.

One `man 1 crontab` later, I had my answer ! ;)
![](/content/images/2020/06/Screenshot_20200622_203829.png)
And reading through it all I saw that :

> Each user  can  have  their  own  crontab

Which means that I could use it without SUDO ! 

I then wanted to see examples of crontab files which I found using the command
`man 5 crontab`

which gave me examples !
![](/content/images/2020/06/Screenshot_20200622_211148.png)
I then ran `crontab -e` to start editing my crontab file !

I then chose which editor I wanted to use and started writing a test command writing a string into a file in the temporary folder(/tmp/) every minutes of every hour of everyday of every weeks of every months of every year hahaha

`* * * * * echo "test" >> /tmp/test.txt`

I closed and saved 
![](/content/images/2020/06/Screenshot_20200622_211733.png)
and one minute later here it was !!
![](/content/images/2020/06/Screenshot_20200622_211857.png)
(edit some days later : I forgot to stop this cron lol and there is now A LOT of test written in this file BE AWARE GUYS hahahaha)

Now, I will add the mysqldump command into my cron tab to make it do its job every week ! 

So as we can see, when we type crontab -e , the header comments gives us good clues on how to setup our system properly. 

![](/content/images/2020/06/Screenshot_20200624_203727.png)
so we got m, h, dom, mon and dow for minutes, hours, days of month, month, days of week... Yeah it's a little bit hard to set... But I found this site which helps a lot !! 
[

Crontab.guru - The cron schedule expression editor

An easy to use editor for crontab schedules.

The cron schedule expression editor

](https://crontab.guru/)
it simplifies greatly the cron values 
![](/content/images/2020/06/Screenshot_20200624_205643.png)
then I made a shell script with the mysqldump command and added it to the cron ( I found it easier to do it this way considering the limitations of crontab regarding the bash scripts )

first I created a BACKUPS folder with
`mkdir BACKUPS`

then I created a bash script that I named sqlBackups.sh
`vim sqlBackups.sh`

in this shell script I coded the command which is pretty simple :

    #!/bin/sh
    
    mysqldump -u YOUR_USERNAME -pYOUR_PASSWORD your_db_name | gzip > ~/BACKUPS/` date +'%m-%d-%Y'`.sql.gz
    

here, the last line name the file with the current date and then zip it using gzip so it doesnt take too much space

Now I have to set the bash script as executable : `chmod +x sqlBackups.sh`

and FINALLY you open crontab editor, and set it up to execute your script every time you need to! I wanted mine to run weekly so I did it like this:
`crontab -e`
`@weekly ~/BACKUPS/sqlBackups.sh`

that<s pretty much all it takes ! :)

I hope you enjoyed the read and feel free to comment any information that you think this article is lacking or your toughts !!

See you soon !

Mathieu2em
