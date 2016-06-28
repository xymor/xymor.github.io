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

### Reading from socket

~~~~ruby
require "socket"
server = TCPServer.open(8080)
loop do
    Thread.fork(server.accept) do |client| 
        reply = "Connected!"
        client.puts(reply)
        client.close
    end
end
~~~~
 The `loop` directive, which is a more terse than `while true`
