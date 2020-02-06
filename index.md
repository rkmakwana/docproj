---
layout: default
title: Home
nav_order: 1
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
permalink: /
---

# GoodTime iOS app
{: .fs-9 }

This documentation is meant for technical guidance for the iOS development team. Although utmost care has been taken to include as much scenarios in this document, if you come across things that are not included and are important to be added, kindly update this document.

{: .fs-6 .fw-300 }

[Get started now](#getting-started){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 } [View it on Gitlab](http://gitlab.vertexplus.inet/gitlab/goodtime){: .btn .fs-5 .mb-4 .mb-md-0 }

---

## Getting started

### Dependencies

GoodTime iOS app is built using **swift** with some **Objective-C** as well.
As of the time of writing this document, the project uses **Xcode 11.3** and minimum supported iOS version is **iOS 11.0**.

The project uses **Cocoapods** as dependency manager.

## About the project

The project is hosted on Gitlab. It is important to note that the `master` branch shall not be used for development. The `dev` branch should be used for ongoing development, and it should be merged with `master` whenever the app is released to the App Store.

Further branches can be created for better clarity and convenience of the team, but should be merged with `dev` at regular intervals.

### Contributing

This documentation is prepared using `Jekyll` static site generator and hosted on Gitlab pages.
For more information, check - [about this documentation](#Contributing).
