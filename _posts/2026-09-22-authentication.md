---
layout: post
title: "Authentication working now"
date: 2026-09-22
---

First thing that I did was follow the tutorial at https://learn.microsoft.com/en-us/aspnet/core/security/authentication/configure-oidc-web-authentication?view=aspnetcore-10.0, which is ultimately enough to set it up but not enough to troubleshoot the apparently herculean task of setting up a correct dev environment. I ran into a dumb error and waited till our intermediary meeting since I thought I'd need Dr. Goadrich to debug it on his admin dashboard like last semester.

On Monday we met and Dr. Goadrich revealed what was the last hurdle to getting authentication to work: use https lol. This had been something that I was annoyed at before, but it was ultimately really simple: do the things in the Microsoft tutorial from Google, but I thought it wasn't working since I was getting an error trying to access `https://localhost:5001`. Turns out that `dotnet run` was just serving http even though my browser wanted https; what worked was deleting the http method in `appsettings.json`. It took me a long time to realize since I thought if it wasn't serving https at all the browser would give a 404 instead, but I guess the protocol in the url is only used for the browser's interpretation of whatever it receives? So authentication works now, and I'm working on fleshing out the implementation in my branch, and I've already committed the minimal changes that allow you to log in and log out.

During that meeting I also inquired about a favicon, and Dr. Goadrich made one: the Hendrix shield + bar but with a cross cut out in the middle. When I got home and checked it, the cross was off-center (how could you) so I remade it and made a PR.

Throughout that now on Monday night I had some hiccups with Git. I had been committing everything to `main` but now I had two changes and remembered Dr. Goadrich saying to make a new branch since PRs apply to entire branches. So I had to reorganize the already existing commits into `auth` and `favicon` and also sync `main` to upstream. Learned (and will hopefully remember) some new commands:
- `git reset [file]` unstage "file"
- `git branch` view branches
- `git checkout [branch]` switch to branch "branch"
- `git checkout -b [branch]` create branch "branch"

Overall, really happy authentication is working now. Once I finish this all these other things up we can start working on the main essential features that were blocked, like only allowing users of certain privileges into certain parts of the website, or only showing assigned evaluation requests to the one it's assigned to. At that point we'll finally have an alpha version. 邁進せいっ!
