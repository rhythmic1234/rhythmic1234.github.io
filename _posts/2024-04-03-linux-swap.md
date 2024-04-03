---
layout: post
title:  "Creating a swap space in Linux"
---

Tried Digital ocean's droplets, the cheapest ones.

And tried to install [n8n](https://n8n.io/) on them via npm and had following error:

```
FATAL ERROR: Reached heap limit Allocation failed - JavaScript heap out of memory
```

As error log tells, I need to tell npm to use less memory. I set heap ceiling limit for node with `NODE_OPTIONS="--max-old-space-size=512"`. Still receiving the same error.

Then I figured out that there is no swap space set in the VM! Probably digital ocean does not set it up since my droplet's RAM is too low.

Anyway, I have learned [how to setup swap space](https://gist.github.com/rhythmic1234/98f12fa7aa4f97edb9e729f897a61f78) in Ubuntu 23.10 today.


After a while, I found out there is a guide on [setting up n8n on a Digital ocean droplet with docker](https://docs.n8n.io/hosting/installation/server-setups/digital-ocean/). Yet, I've learned something today 🙃