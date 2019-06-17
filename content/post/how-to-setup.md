---
title: "How to setup static website like this one on Google Cloud Storage"
date: 2019-06-15
draft: false
tags: [meta]
---

This is an outline of steps I've performed to setup this website. I don't give details much here for each step, but try to refer with links to more detailed explanations. If you're looking for more complete tutorial, try one of the following (from which I compiled my setup):

* https://cloud.google.com/storage/docs/hosting-static-website
* http://evanbrown.io/post/hugo-on-the-go/
* https://geekflare.com/cloud-storage-static-website/ and https://geekflare.com/gcs-site-over-https/
* https://www.tobias-schwarz.com/posts/8/

One important thing that's missing from the above guides is that you shouldn't create CNAME record for your root domain pointing to GCS (instead use "www" subdomain and then redirect from root domain to "www"). While CNAME for root domain works in practice, it [violates an RFC](https://support.dnsmadeeasy.com/index.php?/Knowledgebase/Article/View/14/0/why-cant-i-create-a-cname-record-for-the-root-record) and [breaks email on your domain](https://serverfault.com/questions/91712/dns-using-cnames-breaks-mx-records).

## Basic setup

1. Purchase domain from namecheap.com
1. Sign up for Google Cloud (comes with $300 worth of usage credits for free)
1. Verify domain with Google (https://www.google.com/webmasters/verification/)
1. Create "www.yoursite.com" bucket in GCS, setup access and web pages (https://geekflare.com/cloud-storage-static-website/)
1. Install Hugo and create simple website, then generate static content (http://evanbrown.io/post/hugo-on-the-go/)
1. Sync static content to the bucket with `gsutil rsync` (https://cloud.google.com/storage/docs/hosting-static-website#sharing_your_files)
1. Create CNAME for "www" pointing to GCS and check that website works (https://cloud.google.com/storage/docs/hosting-static-website#cname)
1. Setup redirect from main domain to www

## SSL with Cloudflare

1. Setup Cloudflare for the website (https://geekflare.com/gcs-site-over-https/)
1. Change nameservers in Namecheap to Cloudflare's
1. Setup redirect from main domain to www in Cloudflare (https://support.cloudflare.com/hc/en-us/articles/200172286-Configuring-URL-forwarding-or-redirects-with-Cloudflare-Page-Rules)

I've seen some laggs in content update with Cloudflare caching, but this behaviour is inconsistent and I haven't found a way to disable caching altogether. If this would become an issue, I'd probably remove Cloudflare from my setup.

## Publishing from Git with Travis

1. Create repository on GitHub
1. Add your Hugo content, add generated files to [.gitignore](https://github.com/kholodilov/kholodilov.me/blob/master/.gitignore)
1. Create [.travis.yaml](https://github.com/kholodilov/kholodilov.me/blob/master/.travis.yml) performing hugo build and syncing files to the cloud (https://docs.travis-ci.com/user/deployment/gcs/)
1. Sign up for [Travis CI](http://travis-ci.org) and enable build for your repository
1. Setup access keys in Travis (https://cloud.google.com/storage/docs/migrating#keys)
1. Push changes to website and see it deployed

The pitfall that I've spent some time on is using http://travis-ci.com instead of http://travis-ci.org for automated publishing. The former is paid version with trial limitation, while the latter is free for public repositories.

