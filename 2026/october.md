### October 7

Today I spent several hours struggling with Github Actions (and all sorts of annoying merge conflicts) to set up a simple CI pipeline workflow for the ChurchCMS project. Finally, at 12:49 pm the worfklow run succeeded! Amazing. But...I'm still not even sure if what's in there actually **does** anything. Like, sure. It grabs the latest code, installs npm dependencies, sets up PHP and Laravel, creates a copy of the .env.example file, blah blah. But there are no tests to run, and my local run of PHPStan stopped when it hit 1,000 issues, so I'm not sure that's worthwhile to run, even.

I did learn some good stuff, though. Namely:
- You can't use `uses` and `run` in the same job
- Along those lines, you can't use `run` twice in the same job. Just put the two commands on seperate lines.

Feeding ChatGPT the workflow run error and my yaml file probably saved me hours of headache, so, AI for the win there, I guess.

Struggles aside (honestly, the struggles are part of the fun), it's really cool to have my own little action set up. This has a lot of potential!

Tomorrow I will start in on the Bluehost Deploy/CD pipeline dance. Paul tells me this will be piece of the project I sort of develop in tandem.

### October 8

Most of my morning was spent watching videos on Agile recommended to me by Paul. After lunch I started in on The Big Task: getting the admin ChurchCMS site deployed. I decided that the best course of action would be to initally do it manually, and then, once I'd learned from that whole *process* (yes, I'm anticipating it will be a *process*) work on getting a CD workflow set up.

So I started with a YouTube video, which really didn't make the task seem super difficult. Just like...zip the project, upload it, unzip it, boom!

Unfortunately...my project is a bit more complex. First, there was the task of creating an env file that could be used for the staging environment, and figuring out where to store it. (In my root Bluehost file directory, seems to be the answer?)

Leaving aside the task of figuring out how the app will know where the file is when it's in the staging environment, I next had to figure out how to set up my database on Bluehost -- which meant that I had to import the local DB into what's on Bluehost.

After that I set myself to the task of figuring out what "Configured HTTPS/SSL certificate" from the Security Checklist meant. A very short Google assured me that each Bluehost domain comes configured with its own certificate, so...I don't need to do anything then?

Which then brought me back to the task of figuring out how my app will know where to locate the env file. But first -- I took a brief pause to bomb an interview.

Interview bomb complete (hey, at least the guy was nice to talk to) I hopped back onto the "can I deploy this thing manually?" train. Toot toot! I ended up getting the most help from ChatGPT, who (er...which?) walked me through the process of packaging the files (no explicit command line packaging needed, just zip up the entire project) and getting them put onto Bluehost. Chatty told me I should leave my env file in the root project directory, so after I got everything into the staging folder, I replaced the old file with the fancy new one. (Complete with its own APP_KEY!)

And...voila! 500 error. Lol.

At this point ChatGPT basically became my coworker/mentor and had me walk through everything that could possibly be causing the issue. TURNS OUT all the times I had to add the `--ignore-platform-req=php` when I ran `composer install` should have been my first clue. There was an issue with the version of PHP the app was running on not meshing well with one of the dependencies. *Soooo* I rolled back my PHP version to 8.4 and had composer recreate my vendor folder, zipped the whole thing up again, and put it back onto Bluehost.

And...voila!!!! For real, voila! I had a site live! **Have** a site live!

Well. Sort of. When I try to log in to the admin CMS area, I'm getting yet another error -- this time a 419 saying that my session has expired. I'm having to change a few things in the env file and run some commands to clear the cached configurations, and right now it's 10:22 pm, so, past quittin' time. I'll get back to this tomorrow. And hopefully be able to get into the admin panel and do admin-y stuff!