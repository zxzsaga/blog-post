---
layout: post
title: for vs. forEach - JavaScript
data:  2014-10-28 16:01:00
categories: jekell
published: false
---

I often use the "forEach" method of array in the past. I thought using "forEach" make codes beautiful and I guessed the performance of "forEach" was worse than "for" but not by much. Today I want to test how much the difference of performance is. I looked for a site [jsperf][jsperf] and the benchmark told me the "forEach" is 87% slower than "for", "for" has 10393 ops/sec but "forEach" has 1353 ops/sec. It's too much! Then I test it by myself and found the "for" is about 5 times faster than "forEach". I think I never use forEach again.

[jsperf]: http://jsperf.com/for-vs-foreach/37
