---
layout: post
title: "hello world again"
subtitle: 'Hello world again'
author: "atpking"
header-style: text
tags:
  - Hello world
  - ActionCable
  - prophet-rb
---

@2020-04-19 03:38:24
又开始了新的blog之旅了

## ActionCable

今天研究了一下 ActionCable

一个很有意思的地方是, 之前从来没有人在 terminal 里进行接收 ActiveCable 的消息, 今天顺手写了一下

```ruby
require 'websocket-eventmachine-client'
require 'json'
require 'byebug'
EM.run do

  ws = WebSocket::EventMachine::Client.connect(:uri => 'ws://localhost:3000/cable', headers: {origin: 'http://localhost:3000'})

  ws.onopen do
    puts "Connected"
    ws.send({
      command: "subscribe",
      identifier: "{\"channel\":\"ChatChannel\",\"room\":\"BestRoom\"}"
    }.to_json)

  end

  ws.onmessage do |msg, type|
    puts "Received message: #{msg}"
  end

  ws.onclose do |code, reason|
    puts "Disconnected with status code: #{code}"
    EM.add_timer(2) do
      EventMachine.reconnect "localhost", 3000, ws
      ws.post_init
    end
  end

  EventMachine.next_tick do
    ws.send "Hello Server!"
  end
end
```

这里的重点是, 其实 ActiveCable 是对 ws 的再封装(sub/pub) 的模式
所以在这里的订阅频道, 实际是 发消息

这里理论上就可以做 与 Rails 服务器的交互


## prophet-rb

这是一个 facebook 搞的基于time series 的预测模型的ruby 版本, 看上去似乎有点意思, 可以用在毛驴上.

