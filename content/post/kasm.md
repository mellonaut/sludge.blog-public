+++
title = "Kasm - A Workspace for the People"
description = "You know"
tags = [
    "docker",
    "devops",
]
date = "2022-02-20"
categories = [
    "cloud",
    "devops",
    "containers",
]
image = "https://sludgeassets-sync.s3.us-east-1.amazonaws.com/assets/headers/kasm_door_large.png"
weight = 4
+++

---

# "Nah, you can't install that."

Kasm is really cool. It’s based on Docker and allows you to to stream workspaces over the web like guacomole. You can manage users and groups, custom images, different types of authentication…it's pretty robust. 

Let's take a look at what it's doing. In Portainer we can see it’s a distributed system of containers that reminds me of kubernetes. 



[![N|Solid](/kasm/kasm01.png)](https://sludge.one/kasm)

[![N|Solid](/kasm/kasm02.png)](https://sludge.one/kasm)

[![N|Solid](/kasm/kasm03.png)](https://sludge.one/kasm)

[![N|Solid](/kasm/kasm04.png)](https://sludge.one/kasm)

Let's make ourselves an admin account. We create the account, set the password, go to groups, view the group from the …

Click add user and add your newly made account to admin

[![N|Solid](/kasm/kasm05.png)](https://sludge.one/kasm)

If you're using a hypervisor, now's a good place to take a snapshot in case we break something.

[![N|Solid](/kasm/kasm06.png)](https://sludge.one/kasm)

Run doom on anything:

[![N|Solid](/kasm/kasm07.png)](https://sludge.one/kasm)

Over on Portainer you can see the doom container is now running with a randomly generated name:

[![N|Solid](/kasm/kasm08.png)](https://sludge.one/kasm)

With Vulhub Lab running:

[![N|Solid](/kasm/kasm09.png)](https://sludge.one/kasm)

I think I'n going to put Kasm up as part of my ansible terraform thing. I'm looking ath this role:

https://github.com/MonolithProjects/ansible-kasm_server

Put the files for the roles in a folder in roles…would you believe it.

[![N|Solid](/kasm/kasm10.png)](https://sludge.one/kasm)

Proof!

But then I read further…

[![N|Solid](/kasm/kasm11.png)](https://sludge.one/kasm)

Lets drop the tar file in there and do it like they want'

Lots of errors, kind o got swept up:

[![N|Solid](/kasm/kasm12.png)](https://sludge.one/kasm)

I had to remove all of these "set -o pipefails" 

[![N|Solid](/kasm/kasm13.png)](https://sludge.one/kasm)

It was in the shell command section of the  'install-kasnm.yml' and 'kasm-state'. I also had to clear a couple of space issues with files in here as well, but cant remember which specifically. Now that Its cleaned up, the issue is that 


[![N|Solid](/kasm/kasm14.png)](https://sludge.one/kasm)

I need to figure out what's going on, what's already listening on that port. Or how to put it on another, either one. It has to be traefik. We may not need that one for this VM. Letsnuke the whole VM. We'll spin it back up and not install traefik see what we get

[![N|Solid](/kasm/kasm15.png)](https://sludge.one/kasm)

That seems to be working. The kasm install takes forever and a day from what I remember, but its past there and running smoothly. I found what we need to do, tough.

[![N|Solid](/kasm/kasm16.png)](https://sludge.one/kasm)

In the install.sh script in files. We can change this. We may need to actually package it that way in the tar file, since we have kasm unpacking it. We should be able to do that a different way but going to start there when we need to.

Not sure how we edit galaxy roles, SO Im going to take the role from github and edit it locally:

[![N|Solid](/kasm/kasm17.png)](https://sludge.one/kasm)

Renamed it to fit my ansible- convention for stuff grabbed from galaxy

[![N|Solid](/kasm/kasm18.png)](https://sludge.one/kasm)

See what happens if we edit this main.yml inside the role to bind host port 4443 to container 4443

[![N|Solid](/kasm/kasm19.png)](https://sludge.one/kasm)

[![N|Solid](/kasm/kasm20.png)](https://sludge.one/kasm)

I said "that's what's up" when I saw this. We're good. Except…man, traefik is supposed to be the https proxy. I think we're going to have issues down the road. I think we're going to have to try messing with the default Kasm port. We should be able to make this work

I pushed the kasm branch to github, started a new one for Vault. Im just curious to see how easy this is or if its…let's go.

[![N|Solid](/kasm/kasm21.png)](https://sludge.one/kasm)

Not that easy..

[![N|Solid](/kasm/kasm22.png)](https://sludge.one/kasm)

"msg": "Failed to find handler for \"/home/earth/.ansible/tmp/ansible-tmp-1645295712.3930306-3460-2141914855678/source\". Make sure the required command to extract the file is installed. Command \"/usr/bin/tar\" could not handle archive. Unable to find required 'unzip' or 'zipinfo' binary in the path."

Look that up later.

Started another bracnh probably stupidly off of Vault. But what we did for Vault was simple, if we have to roll back before that that's okay. Im trying to get Cloudflare dns working

[![N|Solid](/kasm/kasm23.png)](https://sludge.one/kasm)

[![N|Solid](/kasm/kasm24.png)](https://sludge.one/kasm)

Ill take it. We just need to figure out how to pull that IP in and we're there. Everything else went smooth enough.

Well, it should be a damn CNAME, so..

[![N|Solid](/kasm/kasm25.png)](https://sludge.one/kasm)

Hmm. New error.

Went through and checked for sensitive info since I was running with secrets the wrong way. You know, development style.  So I'm trashing the instance, I'm commenting out all the cloudflare stuff to come back to ater I finish vault. Push the code.

You know what? We did it dumb, but not the good dumb. So we should just take sludge.one away from Cloudflare and add it to AWS as a custom domain. That'll make it cleaner to spin up with the VM, and then I think we can do something so we can terraform a CNAME on Cloudflare. Hell, a whole proxy network behind cloudflare, we could use c2.sbs on here as well I'd imagine. Planning to do that with CDNs anyway.