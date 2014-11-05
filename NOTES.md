Learning
========

Seems like the media world is a huge mess of stuff, so I plan to explain what I learnt. There are several layers what
 regards to media and formats etc.
 
First of all, the keywords:

 - Codec
 - Container
 - Streamer
 - Protocol
 
Codec
-----
Codecs are just for one thing, for example, video codecs encode video. Those are h264, vp8, vp9, mpeg-2, mpeg-4, 
etc. In the audio part we have the same thing, mp3, aac, wma, etc.

So we have all those parts, and we need now a ...

Container
---------

Containers are the well known formats. These are mp4, mkv, avi, ogg, etc. They specify how to mix all the different 
parts. they do also support extra stuff such as subtitles, menus, chapters, support streaming, etc.
 
We have the data all in a mix, and we need to send it, using a ...

Protocol
--------

The protocols are the well known things, tcp, upd. they just serve for transportation, so, what's the deal?

I skipped one, that you might have noticed, the...

Streamer
--------

These are important because they provide order! You may want to try using udp or tcp directly, 
but the truth is that you need to know *what* to do when something is missing, or which is the order of the stream. 
Also must be taken into account that udp is unordered.

Therefore, we have there, to provide order: HTTP, RTP, RTSP etc.
