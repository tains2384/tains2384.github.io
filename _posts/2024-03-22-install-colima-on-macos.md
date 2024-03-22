---
layout: post
title: Install colima on MacOS Apple Silicon
tags: [colima, docker, docker alternative]
# comments: true
---

<!-- Content here -->

## Steps to install colima on macos

Follow these steps here: https://github.com/abiosoft/colima

## FAQ:

1. If you are facing the error, just go to `~/.docker/config.json` change `credsStore` to `credStore`
   ```bash
  error getting credentials - err: exec: "docker-credential-desktop": executable file not found in $PATH, out: ``
   ```

   <img src="/img/colima-docker-compose-error.png" height="150">
