---
title: "How to setup static website like this one on Google Cloud Storage"
date: 2019-06-15T01:54:54+03:00
draft: false
---

## Basic setup

1. Purchase domain from namecheap.com
1. Sign up for Google Cloud with free credits
1. Verify domain with Google
1. Create "www.example.com" bucket, setup access and web pages
1. Install hugo and create simple website, then generate static content
1. Sync static content to the bucket with gsutil 
1. Create CNAME for "www" pointing to GCS and check that website works
1. Setup redirect from main domain to www

## SSL with Cloudfare

1. Setup Cloudflare for the website
1. Change nameservers in namecheap
1. Setup redirect from main domain to www in Cloudflare


## Publishing from Git with Travis

1. Create repository on GitHub
1. Create .gitignore and push
1. Sign up for Travis
1. Create .travis.yaml
1. Push changes to website


https://geekflare.com/cloud-storage-static-website/

http://evanbrown.io/post/hugo-on-the-go/

