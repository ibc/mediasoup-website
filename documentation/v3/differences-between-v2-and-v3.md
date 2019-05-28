---
title : Differences Between v2 and v3
---


# Differences Between v2 and v3

Both mediasoup v3 and mediasoup-client v3 (in addition to the new libmediasoup C++ library) are, in short, much more low level than their corresponding v2 versions and come with tons of improvements and new features. The table below just exposes the most attractive ones.

----

<div markdown="1" class="table-wrapper L1-small L4">

Feature                 | v2 | v3 | Description
----------------------- | -- | -- | -------------------------------
mediasoup protocol      | <span class="checkbox on"/> | <span class="checkbox"/> | v2 comes with a set of [JSON messages](https://mediasoup.org/documentation/v2/mediasoup-protocol/) that must be blindly exchanged between client and server. While this makes the client side "theoretically easier" it difficults the server side logic.<br>In v3, instead, mediasoup provides a comprehensive low level JavaScript API in both client and server sides, so the application knows which exact kind of information it exchanges between client and server.
Peers                   | <span class="checkbox on"/> | <span class="checkbox"/> | v2 includes the concept of "peers" in its API. A peer is just a container that holds transports, producers and consumers (in fact, a peer just exists in the mediasoup JavaScript land).<br>v3 gets rid of "peers" and enforces a low level API based on transports that hold producers and consumers. It's up to the application to handle "peers" at signaling level (if needed) and associate mediasoup entities with those "peers".
Routers                 | <span class="checkbox"/> | <span class="checkbox on"/> | In v2 a mediasoup room holds peers. In v3, room has been renamed to router and does not hold peers but transports. Renaming it to router makes it fit much better to what it really does.
Plain RTP injection     | <span class="checkbox"/> | <span class="checkbox on"/> | v3 provides a unified API to inject or extract audio/video into/from a mediasoup router using plain RTP or WebRTC transports. This makes it easy to integrate well known softwares such as FFmpeg or GStreamer into a mediasoup based application.
Multiple binding IPs    | <span class="checkbox"/> | <span class="checkbox on"/> | In mediasoup v2 just a static IPv4 and IPv6 pair can be assigned to all transports. In v3, instead, each transport can be provided with multiple and different IPv4 and/or IPv6 addresses. This enables scenarios in which media is conveyed through public and private network interfaces.
Per worker settings     | <span class="checkbox"/> | <span class="checkbox on"/> | mediasoup v2 exposes a `Server` class that internally handles N workers (media subprocesses) sharing them all the same settings. In v3 the application creates each worker independently and can assign different settings to them (such as ports range, log level and so on).
Horizontal scalability  | <span class="checkbox"/> | <span class="checkbox on"/> | By using the new pipe transports in v3, two mediasoup routers running in the same or different hosts can be interconnected at media level, increasing the broadcasting capabilities by enabling usage of multiple CPU cores even in different machines. More info about this [here](https://mediasoup.org/documentation/v3/scalability/).
Sender side BWE         | <span class="checkbox"/> | <span class="checkbox on"/> | mediasoup v3 implements sender side bandwidth estimation to automatically switch between SVC and simulcast spatial/temporal layers in consumers thus accommodating the total transport bitrate to the bandwidth available in the receiver endpoint.
Unlimited video layers  | <span class="checkbox"/> | <span class="checkbox on"/> | mediasoup v2 limits the number of simulcast video streams to 3 ("low", "medium" and "high"). mediasoup v3 can handle unlimited spatial and temporal layers and refers to them by their numeric index (from 0 to N).
Stream score            | <span class="checkbox"/> | <span class="checkbox on"/> | mediasoup v3 notifies the application with scores for every RTP stream (in producers and consumers), allowing the application to know how the overall transmission quality is in every sender and receiver.

</div>
