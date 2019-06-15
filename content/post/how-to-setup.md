---
title: "How to setup static website like this one on Google Cloud Storage"
date: 2019-06-15
draft: false
tags: [meta]
---

## Basic setup

1. Purchase domain from namecheap.com
1. Sign up for Google Cloud with free credits
1. Verify domain with Google
1. Create "www.example.com" bucket, setup access and web pages (https://geekflare.com/cloud-storage-static-website/)
1. Install Hugo and create simple website, then generate static content (http://evanbrown.io/post/hugo-on-the-go/)
1. Sync static content to the bucket with gsutil 
1. Create CNAME for "www" pointing to GCS and check that website works
1. Setup redirect from main domain to www

## SSL with Cloudfare

1. Setup Cloudflare for the website (https://geekflare.com/gcs-site-over-https/)
1. Change nameservers in Namecheap
1. Setup redirect from main domain to www in Cloudflare (https://support.cloudflare.com/hc/en-us/articles/200172286-Configuring-URL-forwarding-or-redirects-with-Cloudflare-Page-Rules)


## Publishing from Git with Travis

1. Create repository on GitHub
1. Create .gitignore and push
1. Sign up for Travis
1. Create .travis.yaml (https://docs.travis-ci.com/user/deployment/gcs/)
1. Setup access keys (https://cloud.google.com/storage/docs/migrating#keys)
1. Push changes to website
