---
layout: post
title: "YikYak moved to Google Cloud from AWS"
keywords: "YikYak, Google Cloud, AWS"
published: true
comments: true
---

[YikYak](https://www.yikyak.com/home), a popular application around geo-tagged content moved to GCP from AWS, and [we have got a blog post](https://medium.com/yik-yak-eng/migration-to-google-cloud-platform-overview-9b5e5c17c368) out of it giving a high level view of their before-after states.

It makes for an interesting read and addresses a few issues, like AWS pricing tiers, PHP weak typing related issues, performance optimizations to be had from Google's geo-querying tools, and things you absolutely need to take care of when moving your entire infrastructure around at this massive scale.

I recommend reading through the 10-or-so minute read if you have ever wanted to know what kind of issues one could run into while switching providers, or the optimizations you can start to think about.
