---
layout: post
title:  "Embedded Browser Study"
tags:   [chromium,cef,electron,node]
---



## Chromium Embedded Framework (CEF) for C++

Getting started is quite straightforward following the intructions on [CEF project page]. Just clone the [CEF project on GitHub] into a local directory (or fork it and clone your own repo) and then run [CMake] to generate the project files for your platform and IDE of choice. In my case, the platform is Debian Linux (Ubuntu) on commodity x64 hardware (acer swift-3 notebook) and the IDE of choice is JetBrain's [CLion] \("Intellij for C++"), which has built-in CMake support. Just opening the directory with the cloned repo in CLion started the CMake generator, downloaded the CEF dependencies, and allowed me to run examples/minimal straight away. Nice! 

## Node.js & Electron

An Electron app is a node.js app 

```bash
sudo apt install nodejs npm
```


## Qt WebEngine

Valued colleagues told me they use Qt WebEngine in their product, so this might be worth checking out, too. After reading [Fiber blog], I opted examining [CEF], first.

[CEF]: https://en.wikipedia.org/wiki/Chromium_Embedded_Framework
[CEF project page]: https://bitbucket.org/chromiumembedded/cef-project
[CEF project on GitHub]: https://github.com/chromiumembedded/cef-project
[CMake]: https://en.wikipedia.org/wiki/CMake
[Clion]: https://www.jetbrains.com/clion/
[Fiber blog]: https://kver.wordpress.com/2015/08/05/fiber-update-webengine-vs-cef/
[Electron]: https://en.wikipedia.org/wiki/Electron_(software_framework)


