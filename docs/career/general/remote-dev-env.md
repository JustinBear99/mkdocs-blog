---
date:
  created: 2023-11-24
  updated: 2023-11-28

description: >
  Motivation and guide on hosting remote (cloud) developmenet environment using machine of your own.

tags:
    - Cool
    - Code Server
    - Ngrok

comments: true
---
# Self-hosted Cloud Development Environment

## What is it?

As more and more work flows such as building and deployment have been moved onto the cloud, further moving coding to the remote is not a strange idea. This movement ensures that developer can have consistent working experience through different devices. Many cloud development environment (CDE) like [Github Codespaces](https://github.com/features/codespaces) and [Gitpod](https://www.gitpod.io/) have been released for a while. However, the free tier membership has very limited use time, so I start to research on how to achieve it on my own device.

## All You Need is a PC

> Disclaimer: my approach includes only the **coding** part. Following steps like building and deployment still require to DIY or other existing tools. :)

Basically we need an multifunctional IDE accessible from browser and have to expose it onto public network (ingress), so here comes [code server](https://github.com/coder/code-server) and [Ngrok](https://ngrok.com/). BTW, both are free FOREver (?).

**Code server** runs VSCode on your machine and can be accessed through browser which means that you can benifit from VSCode's powerful extensions. I think almost any kinds of development requirements can be fulfilled, from linter, git to container (at least terminal). **Ngrok** then provide secure ingress to safely connects to your home machine from everywhere. Recently, they even provide free static domain name for everyone (it was randomly generated every time). Although you can't name it, it's still awesome!

The overall setup is very easy and take my own as example. I use a M1 mac mini (8/128GB) as my host server which also cover my use at home running a bunch of APPs in background.
1. Run `curl -fsSL https://code-server.dev/install.sh | sh` to install latest code-server.
2. Open a terminal and run `code-server` and everything is ready-to-go. You can login with password or from other [options](https://coder.com/docs/code-server/latest/guide#external-authentication).
3. Create account for Ngrok
4. [Download](https://ngrok.com/download) and configure it.
5. Start coding!

Have been using these for a couple of months and they works perfect and steady. 😊

## Next Step

Both code-server and Ngrok are running in Mac OS rn in my setup. Maybe one day I'll move them to a dedicated container based on Linux and add some useful CI/CD tools. But that should happend when I'm working on larger side project. XD