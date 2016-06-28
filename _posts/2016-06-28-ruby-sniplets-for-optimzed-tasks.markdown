---
published: true
title: Ruby sniplets for optimized tasks
layout: post
---
### Reading a file

~~~~ruby
enum = file.lines
100.times{enum.next} # offset 100 lines
enum.take(100) # take the next 100 
 	
~~~~