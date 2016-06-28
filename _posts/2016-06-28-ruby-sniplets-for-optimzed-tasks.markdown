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
 The `loop` directive, which is more terse than `while true`

### Dynamic dispatch

This is my solution to the coderbyte's Reverse polish notation challenge. It illustrates ruby's send method dispatch

~~~~ruby
  expression = "+ - 1 2 5"
  operands = []
  evaluated = []
  
  expression.each do |c|
    case c 
    	when /\d/
      		evaluated.push(c.to_f)
        when "-", "/", "*", "+", "**"
      		operands = evaluated.pop(2)
      		evaluated.push(operands.first.send(c, operands[1]))
    end 
  end  
  evaluated.first.to_i
~~~~