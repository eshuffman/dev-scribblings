### October 7

Today I spent several hours struggling with Github Actions (and all sorts of annoying merge conflicts) to set up a simple CI pipeline workflow for the ChurchCMS project. Finally, at 12:49 pm the worfklow run succeeded! Amazing. But...I'm still not even sure if what's in there actually **does** anything. Like, sure. It grabs the latest code, installs npm dependencies, sets up PHP and Laravel, creates a copy of the .env.example file, blah blah. But there are no tests to run, and my local run of PHPStan stopped when it hit 1,000 issues, so I'm not sure that's worthwhile to run, even.

I did learn some good stuff, though. Namely:
- You can't use `uses` and `run` in the same job
- Along those lines, you can't use `run` twice in the same job. Just put the two commands on seperate lines.

Feeding ChatGPT the workflow run error and my yaml file probably saved me hours of headache, so, AI for the win there, I guess.

Struggles aside (honestly, the struggles are part of the fun), it's really cool to have my own little action set up. This has a lot of potential!

Tomorrow I will start in on the Bluehost Deploy/CD pipeline dance. Paul tells me this will be piece of the project I sort of develop in tandem.