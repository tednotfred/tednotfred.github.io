---
title: Bugzilla Lost Passwords
layout: post
tags: [server]
---
## Resetting a lost passwordin Bugzilla.


I had a situation where we had an old Bugzilla server that hadn’t been used for several years. As these things often happen, the “powers that be” suddenly decided we need that server to be back up and running NOW. Of course, nobody could remember their passwords any more and the email password mechanism had stopped working.


A Google search could only seem to turn up suggestions that started with “login to an admin user…”. Yeah, if I could do that I wouldn’t really have problem would I?


Anyway the solution was pretty easy actually.


This is a dangerous solution that leaves the admin user exposed for a short time. You should take reasonable precautions to prevent access until finished. Either with firewall rules or via an Apache .htaccess rule.


Sign on to Mysql via the command line on the server in question.


~~~sql

USE bugs; (the bugzilla database)
UPDATE profiles SET cryptpassword=null WHERE userid=1;
QUIT;

~~~


**NOTE:**  *userid is the id of an admin user*

You can now login as that admin user with no password *see I told you it was dangerous* .


As admin you can change the password of another user to a password you can rememember, so go ahead and do that.


Now if you go back into the database and list everything you will see the encrypted passwords.


Now just set the password for your admin user and use the encrypted string in place of null in the above SQL statement.


Once you have set the encrypted password you should be able to login as the admin user using the password you set and you can even change the password at this point.
