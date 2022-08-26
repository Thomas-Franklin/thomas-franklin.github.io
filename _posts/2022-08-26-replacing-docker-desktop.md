---
layout: post
author: Thomas
title: Moving from Docker Desktop
categories:
- blog
- info
- docker
tags:
- updates
- docker
---

Like a lot of developers, [Docker](https://www.docker.com/) has been an important tool of my workflow but with [recent pricing updates](https://www.docker.com/blog/updating-product-subscriptions/) (yes, ~1 year ago is recent 😄) when working for a company continued use of [Docker Desktop](https://www.docker.com/products/docker-desktop/) would need to be licensed, while remaining free for personal use.

As like most companies, the company laptop offerings typically involve a Mac Pro which Docker Desktop is generally the fastest way of getting access to the `docker` CLI etc. but for me I generally only use the CLI I sort of by default downloaded the Docker Desktop for convience of running Docker in Mac. Lately I have been wondering - is it as straightforward to not use Docker Desktop but still get the benefits of `docker` - short answer is YES.

Looking online there is tons of ready made solutions, but I wanted one which was as straightforward as downloading Docker Desktop and getting started, one which kept coming up was [colima](https://github.com/abiosoft/colima) which looked promising, but others stumbled upon [rancher desktop](https://rancherdesktop.io/) which also looked promising - so I got to work.

1. First order of business was cleaning up Docker Desktop
    * Stopping it (if running)
    * Moving the Docker.app to trash
    * Cleaning any caches, supporting, library files
1. Once it was cleaned up I now needed to get access to the CLI
    * For brew users, I simply done a `brew install docker`
1. Download Rancher Desktop for your OS (Mac Silicon, or Intel)
    * During setup I disabled `kubernetes` - I use other tools for `kubernetes` based workflows
    * Then set the container runtime to `dockerd`
    * Wait for the VM to start, similar to Docker Desktop for running Docker on Macs a Linux VM is required
1. For me the docker.config was a bit malformed, so a quick 
    ```
    sed -ie 's/credsStore/credStore/g' ~/.docker/config.json
    ```
    * Fixed up the `error getting credentials - err: exec: "docker-credential-osxkeychain": executable file not found in $PATH, out: ` when trying to download images
1. After this I could continue to use my typical docker CLI workflows as normal


Caveats: 
* Rancher Desktop is not as fluid as Docker Desktop in terms of what it offers
    * Docker Desktop really is very intuitive if you're not comfortable with the command line, i.e. you can see running containers, access ports, shell in to them etc. at the click of a button


For me, the benefits of Docker Desktop were often lost, as I always found myself going straight to the terminal to perform these tasks. For others, possibly the benefits of Docker Desktop is worth a license, but I cannot justify it 😀
