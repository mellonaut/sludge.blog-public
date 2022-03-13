+++
title = "Serverless Blog - Part I"
description = ""
tags = [
    "blog",
    "cloud",
    "devops",
]
date = "2022-02-05"
categories = [
    "blog",
    "cloud",
    "devops",
]
image = "https://sludgeassets.s3.us-east-1.amazonaws.com/s3_blog/devswarm.png"
weight = 2
+++

---

<b>
# 'CDN-based Blog'

## _"Day 1: Building the blog..."_ 

Back to the basics https://pakstech.com/blog/blog-with-hugo/

Chosed these two themes to play with 
kc0bfv/ticky_tacky_dark: A multi-page Hugo theme, in dark colors, where the list page displays a set of image buttons linking to your sub-pages. 

https://github.com/sharadcodes/hugo-theme-serial-programmer for backup

Choco installed gimp so I can resize some images
I have the theme, Im reading the themes specific instruction. Each theme has its own way it wants to do things. It looks like the header image serves out of the img folder like such:

Example site:
[![N|Solid](/s3_blog/blog01.png)](https://sludge.one/s3blog)
[![N|Solid](/s3_blog/blog02.png)](https://sludge.one/s3blog)
[![N|Solid](/s3_blog/blog03.png)](https://sludge.one/s3blog)

Header images are, optimally, 950x200 pixels. Specify these in the site configuration as a list of image URLs with option images. One will be randomly selected on page load.

[![N|Solid](/s3_blog/blog04.png)](https://sludge.one/s3blog)
[![N|Solid](/s3_blog/blog05.png)](https://sludge.one/s3blog)
[![N|Solid](/s3_blog/blog06.png)](https://sludge.one/s3blog)
[![N|Solid](/s3_blog/blog07.png)](https://sludge.one/s3blog)

Saved as project files and exported as well under "header1" "header2" right outside the actual project itself. Under OneDrive I have a Code workspace, a Blog folder, and these sitting right outside "blog.folder" on my dev machine.

Cut my lil gothy wolf image into slices to be used for the header image pool. Hugos going to grab at random images from the folder that (I think) are tagged for headers. Some way or another, we'll get there though.

Favicon, why not:

[![N|Solid](/s3_blog/blog08.png)](https://sludge.one/s3blog)

 Lets copy some files into the static directory and start adding them to our config.toml

[![N|Solid](/s3_blog/blog09.png)](https://sludge.one/s3blog)

Started making buttons for navigation. 300x300 supposed to be but mine..well let's see. Next steps are figuring out how to do these sub pages and navigatew the, via these button images.

[![N|Solid](/s3_blog/blog10.png)](https://sludge.one/s3blog)

The --- need to be before and after your page set up. This is where you set your titles, weights, etc.

Then we'll spin up Hugos awesome built in development server with "hugo server -D', and note the pain that is YAML. You can see that the server wouldn't build. This is because I had a couple blank spaces and a linebreak after line 13 I didn't know was breaking the build. YAML is so touchy.

[![N|Solid](/s3_blog/blog11.png)](https://sludge.one/s3blog)

The server will monitor chasnges made to files in the project directory and automagickally re-serve them:

[![N|Solid](/s3_blog/blog12.png)](https://sludge.one/s3blog)
[![N|Solid](/s3_blog/blog13.png)](https://sludge.one/s3blog)

I want to lock that image as the main banner and have the other pages randomly pull from that img folder.  And those are some ugly ass buttons.

As I create placeholder files for sections of the blog, the server is listening for changes saved to the filesystem. So when I ctrl+s in vs code, it appears, automagickally before our very eyes. I feel like the guy who looked at the Holy Grail in Raiders. 

[![N|Solid](/s3_blog/blog14.png)](https://sludge.one/s3blog)
[![N|Solid](/s3_blog/blog15.png)](https://sludge.one/s3blog)


## _"Day 2: We should probably start thinking about terraform..."_ 


Working on this serverless blog project. We may need a webhook. I wonder if we can just put this in a terraform workspace. We may be able to get around this webhook if it comes to it. Doesn’t it handle the “github action” triggering? Guess we’ll find out. Heres one thing working with cloud…
This project I’m using for reference is 3 years old. Terraform has changed a lot since then. It’s telling me to put them in  the required providers block… we should investigate. I THINK I’ve only seen this done with required_providers block. I don’t think I even looked at Terraform 3 years ago. So this blog post will also be about breathing new life into aging cloud projects. Code rot they call it. Let’s do our part!  

Terraform Providers – Every resource in a terraform project (or “configuration”) must be associated to some Provider. Providers (or “Provider Configurations”) are GLOBAL to the entire Terraform project. They can be shared across multiple modules using, say, AWS. We define these in our “root module” (often main.tf, here I’m using root.tf just to illustrate).
If a module is going to be used by further modules in the project, it must not contain any “provider” blocks. Child modules will inherit from the root module.

[![N|Solid](/s3_blog/blog16.png)](https://sludge.one/s3blog)

The name given in the block header “google” is the “local name” of the provider. This should already have been declared in a required providers block. For example you may have…and this is from Hashi’s docs…


[![N|Solid](/s3_blog/blog17.png)](https://sludge.one/s3blog)

I think this gives me an idea about our project. I think we need to put the cloudflare/cloudflare as a required provider up top. I wonder why it wasn’t necessary three years ago when this github project was finished, what changed it. So make a note, when we see that Cloudflare error again later we just need to definite it (and aws, and github) as required providers and set the plugins’ versions ther

[![N|Solid](/s3_blog/blog18.png)](https://sludge.one/s3blog)

ANDDDDDDDDDDD:

[![N|Solid](/s3_blog/blog19.png)](https://sludge.one/s3blog)

Guess we better run that.

[![N|Solid](/s3_blog/blog20.png)](https://sludge.one/s3blog)

Let’s see if our cloudflare provider trouble is in that static site module. It is, and I’m not sure how to proceed. Remember we talked about inheriting providers? I think that’s what’s happening here. I think it’s trying to call an older hashicorp/cloudflare provider from this old module on github. Not sure where to go from here, except back into the Docs. I’m Going back, back basic, even basicer….
https://learn.hashicorp.com/tutorials/terraform/cloudflare-static-website?in=terraform/aws
Reduce the complexity, see it done a slightly different way. I don’t know how it works for everyone else, but my learning curve starts with compare, settles with contrast and maybe it’s something by the time I can do both for someone else. Have to see where it fizzles and breaks. 


[![N|Solid](/s3_blog/blog21.png)](https://sludge.one/s3blog)
[![N|Solid](/s3_blog/blog22.png)](https://sludge.one/s3blog)
[![N|Solid](/s3_blog/blog23.png)](https://sludge.one/s3blog)
[![N|Solid](/s3_blog/blog24.png)](https://sludge.one/s3blog)

Had a bucket with that name. It's a good idea to get in the habit of running terraform destroy –auto-approve to keep stuff like this from happening. I'll go home for the weekend and forget something test mode was still up.
Got past that just to find...

[![N|Solid](/s3_blog/blog25.png)](https://sludge.one/s3blog)
[![N|Solid](/s3_blog/blog26.png)](https://sludge.one/s3blog)

The struggle is real!

Let's pivot over to the graphics for a bit and let the back-mind do it's thing. 

[![N|Solid](/s3_blog/blog27.png)](https://sludge.one/s3blog)

We need images of 300x150 for the small sidebar buttons inside the article. We need 300x500 for the big navigation buttons. We need 950x200 for the headers up top. Heres how I made some quick art for the site. Take some free art you like, I like to search google for creative commons licensed stuff I like by keywords. Put all those in a 'pictures' folder and create a 'graphics' one. We're going to create a template in GIMP at each of those sizes. Then..and this is janky..we're gonna paste in the photo we want to use. Now…lol. Take the image, move it under the templated area until you get a snapshot you like..let me see…


[![N|Solid](/s3_blog/blog28.png)](https://sludge.one/s3blog)
[![N|Solid](/s3_blog/blog29.png)](https://sludge.one/s3blog)
[![N|Solid](/s3_blog/blog30.png)](https://sludge.one/s3blog)

Now you can export whatever is inside that frame to a jpg. I like to take "circuit" for example. Make a few header sized cuts, a few big button sized cuts, usually more small buttons just to have. If you take a handful of images that sort of thematically or colorwise work together you can make a bunch of art for your theme. Theres probably better ways this is just what I came with up over the weekened

[![N|Solid](/s3_blog/blog31.png)](https://sludge.one/s3blog)
[![N|Solid](/s3_blog/blog32.png)](https://sludge.one/s3blog)
[![N|Solid](/s3_blog/blog33.png)](https://sludge.one/s3blog)

See? We got a little theme going. Later when I moved to another theme I realized many of them do something like this for you, or can. I did it the angelfire way.

[![N|Solid](/s3_blog/blog34.png)](https://sludge.one/s3blog)
[![N|Solid](/s3_blog/blog35.png)](https://sludge.one/s3blog)

Kinda running two styles here but I hope I can mix them enough…one look for building, one for pentesting, for code, for music, etc. Headers randomly pull from an array of photos you define in the config.toml. 

## _"Day 3: Back on the Blog..."_ 

Started fresh and unfrustrated.  got it working, and broke it again, and wasn't even cool enough to document. Kinda wish I had, though. Www was broken because I was trying to use a subdomain like cloudmagick.sludge.one. Terraform was correctly putting the bucket as cloudmagick.sludge but cloudflare was still trying to redirect "www". So we could only get to the root sludge.one if we came at it directly. 

This one may have been easy. Hugo renders everything down to a "public" folder. I copy the contents from that folder to "website" that the Tform script uses. I think I left the old and new versions together, probably a mess for Hugo to figure out. Cleared out "website" and dumped the contents of "public" in place.



[![N|Solid](/s3_blog/blog36.png)](https://sludge.one/s3blog)

Now, I just destroyed and reapplied. Normally I would use:

aws s3 cp website/ s3://$(terraform output -raw website_bucket_name)/ --recursive

To copy that "website" folders contents up to the s3 created by terraform. This ain't best practice. I don't know if anyone would really suggest putting your website in the same folder as your terraform configuration, but we're just playing around (in production?). I want to see what it already did. 

[![N|Solid](/s3_blog/blog37.png)](https://sludge.one/s3blog)

Both empty.

[![N|Solid](/s3_blog/blog38.png)](https://sludge.one/s3blog)

No juice on the link, but its up...

[![N|Solid](/s3_blog/blog39.png)](https://sludge.one/s3blog)

S3'ed the files to that bucket...

Man we're good! Up and working. Let's see about getting some images on these pages.

[![N|Solid](/s3_blog/blog40.png)](https://sludge.one/s3blog)

Man…I don't like our theme. It's a little too…tacky. GET IT. I think I will keep it for a music blog theme. It works great for album reviews. I want somewthing a little more in line with what I'm doing.

[![N|Solid](/s3_blog/blog41.png)](https://sludge.one/s3blog)

I ended up making an S3 bucket solely for graphics, public readable and use that to host the images and just link to them in the actual blog pages rather than deal with the paths inside the project folders. This means we can really easily use them for other stuff or move the project around with less trouble.

Having trouble with the blog, my browsing returned a good thing that was bothering me before:

[![N|Solid](/s3_blog/blog42.png)](https://sludge.one/s3blog)

This is why I moved to serving graphics in the s3 itself. For some reason…its not loading on the web.

[![N|Solid](/s3_blog/blog43.png)](https://sludge.one/s3blog)

Because, the posts are relative to the root of your website.
When you use Hugo with the option --server, as a server to create your files, Hugo considers the folder content as the root. It knows that if there’s files image into static/images, it must bind as-is.
When you publish with hugo command, all datas are writed on public folder. This one becomes the root, within which folders posts, images and others are at the same level.

[![N|Solid](/s3_blog/blog44.png)](https://sludge.one/s3blog)

Cool, that works, and that post was very helpful. We have a backup if S3 gets too weird.

Had some thoughts about s3 and pricing…. Decided it would be best to store the images within the site itself for a number of reasons. Cost, complexity… down the line that may be the better way. This was easy to fix, though. My folder structure was the same <S3 URL>:/s3_blog/<image> now that S3 url will just be the static folder of the Hugo project. We put s3_blog folder in there, and we just use VS Code to change all occurences of the URL part to "/" since the paths…

[![N|Solid](/s3_blog/blog45.png)](https://sludge.one/s3blog)