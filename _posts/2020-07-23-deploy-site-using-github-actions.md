---
layout: post
title: 'Deploy site using Github Actions'
date: '2020-07-23'
author: Timoteo Ponce
tags:
- guide
---

A while ago I had a personal site in some obscure Russian hosting site, I don't even remember if I have paid for that hosting
or if it was something with ads. Nevertheless, since then the idea of having a public and personal website has always attracted me.

So, once the motivation is set, a new site is gonna be created, this is how we can proceed to create a personal website:

<img src="/assets/img/site_preview.png" height="500" alt="Site preview at https://timoteoponce.com">

## Domain

The first step in all web-related ideas is to buy a domain, nothing is really done unless it's public. In the past it was really complex
to get a domain, but nowadays it's quite simple, while there are many choices to buy and manage domains, [Namecheap](https://www.namecheap.com/) it's one of the 
cheapest ones. Our domain at [https://timoteoponce.com](https://timoteoponce.com) costed around 12 USD a year, so we bought it. 

## Server host

Now, on the hosting part we have many options as well, some of my favourites ones these days are:

  -  [Digital Ocean](https://www.digitalocean.com/)
  -  [Linode](https://www.linode.com/)

Why these providers? Because they provide you empty servers, we must handle everything from scratch. We went with **Digital Ocean** with the cheapest server as well 
and proceeded to configure a simple **Ubuntu Server** instance.

## Web server

Once that is done, we need to install a web server, while **Apache** is still the great player, (Nginx)[https://nginx.com] is a superb tool for the matter, following the following tutorial was just enough:

  -  [Install Nginx](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-18-04)

## Link the domain to the machine

This was a piece of cake (this used to be a bit hard back in the day) by following the official guide:

  -  [Link Namecheap to Droplet](https://www.digitalocean.com/community/tutorials/how-to-point-to-digitalocean-nameservers-from-common-domain-registrars#registrar-namecheap)

## HTTPS

Another thing that is quite simple and mandatory for any site now, HTTPS, and it's so simple. Proceeded to perform this task with the amazing [Let's Encrypt](https://letsencrypt.org):

  -  [Secure Nginx with Let's Encrypt](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-18-04)

## Dynamic or static content?

Finally, we have the whole infrastructure is ready, we can finally start adding some content to our site!

What to do then? In the past, to install a CMS would have been the first choice, but not all sites require the overhead and complexity of a full CMS, our intent is mainly to publish content that's mostly static, and being ourselves in the development environment, something like a [static site generator](https://www.staticgen.com) is a great approach.

Once our content is set (I'm using [Jekyll](jekyllrb.com)) we push it to [Github](https://github.com) and then create an action to deploy it to our shiny server, yet again, here's the guide to do it:

  -  [Deploy a static site using Github Actions](https://www.digitalocean.com/community/questions/how-to-deploy-using-github-action)