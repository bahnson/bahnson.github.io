---
layout: post
title:  "Embedded Browser Study"
tags:   [chromium,cef,electron,node]
---



## Chromium Embedded Framework (CEF) for C++

The [Chromium Embedded Framework] allows embedding Chromium (core of the Chrome browser) in own applications, that may themselves be written in any of the "common" application programming languages.
I opted for C++, since this is CEF's native language. 

Getting started is quite straightforward following the intructions on [CEF project page]. Just clone the [CEF project on GitHub] into a local directory (or fork it and clone your own repo) and then run [CMake] to generate the project files for your platform and IDE of choice. In my case, the platform is Debian Linux (Ubuntu) on commodity x64 hardware (acer swift-3 notebook) and the IDE of choice is JetBrain's [CLion] \("Intellij for C++"), which has built-in CMake support. Just opening the directory with the cloned repo in CLion started the CMake generator, downloaded the CEF dependencies, and allowed me to build and run examples/minimal straight away. Nice!
CLion, however, didn't find CEF's symbols in the first place. I fixed this by adding the include directory of the actually downloaded CEF library in CMakeLists.txt in the project root:

```cmake
include_directories(${CMAKE_SOURCE_DIR}/third_party/cef/cef_binary_3.3538.1852.gcb937fc_linux64)
```

## Node.js & Electron

Electron allows embedding Chromium in node.js applications. [Zeke's talk about Electron] gives an excellent introduction to Electron, and its roots and history.

```bash
sudo apt install nodejs npm
mkdir -p path/to/app && cd path/to/app
...
```


## Qt WebEngine

Valued colleagues told me they use Qt WebEngine in their product, so this might be worth checking out, too. After reading [Fiber blog], I opted examining [CEF], first.

[Chromium Embedded Framework]: https://en.wikipedia.org/wiki/Chromium_Embedded_Framework
[CEF project page]: https://bitbucket.org/chromiumembedded/cef-project
[CEF project on GitHub]: https://github.com/chromiumembedded/cef-project
[CMake]: https://en.wikipedia.org/wiki/CMake
[Clion]: https://www.jetbrains.com/clion/
[Fiber blog]: https://kver.wordpress.com/2015/08/05/fiber-update-webengine-vs-cef/
[Electron]: https://en.wikipedia.org/wiki/Electron_(software_framework)
[Electron's bad parts]: https://hackernoon.com/electron-the-bad-parts-2b710c491547
[Zeke's talk on Electron]: https://www.youtube.com/watch?v=FNHBfN8c32U&t=1948s


