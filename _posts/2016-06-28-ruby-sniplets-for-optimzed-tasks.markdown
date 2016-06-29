---
published: true
title: Ruby sniplets for optimized tasks
layout: post
tags: [ruby, rails, performance]
categories: [ruby]
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
 The `loop` directive is more terse than `while true`

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

### Rails gotcha, avoid active record magic when dealing with bulk objects

 Consider you are trying to recover all tags, you're inclined to write:

~~~~ruby
tasks = Task.find(:all, :include => :tags)
~~~~

But tags are often value objects, only their name matters and there's often no logic attached to this state. So consider using instead: 

~~~~ruby
tasks = Task.select <<-MLINE
      *,
      array(
        select tags.name from tags inner join product_tags on (tags.id = products_tags.tag_id)
        where products_tags.product_id=products.id
      ) as tag_names
    MLINE
~~~~
It's much less sexy but much faster. 