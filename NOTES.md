Learning
========
These are the notes I have been taking about what I am learning with this project

Media
-----
Seems like the media world is a huge mess of stuff, so I plan to explain what
 I learnt. There are several layers what regards to media and formats etc.
 
First of all, the keywords:

 - Codec
 - Container
 - Streamer
 - Protocol
 
### Codec
Codecs are just for one thing, for example, video codecs encode video. Those 
are h264, vp8, vp9, mpeg-2, mpeg-4, etc. In the audio part we have the same 
thing, mp3, aac, wma, etc.

So we have all those parts, and we need now a ...

### Container
Containers are the well known formats. These are mp4, mkv, avi, ogg, 
etc. They specify how to mix all the different parts. they do also support 
extra stuff such as subtitles, menus, chapters, support streaming, etc. 

We have the data all in a mix, and we need to send it, using a ...

### Protocol
The protocols are the well known things, tcp, upd. they just serve for 
transportation, so, what's the deal?

I skipped one, that you might have noticed, the...

### Streamer 
These are important because they provide sequence! You may want to try using udp
or tcp directly, but the truth is that you need to know *what* to do when 
something is missing, or which is the order of the stream. Also must be taken
 into account that udp is unordered. 
 
Therefore, we have to provide sequence: HTTP, RTP, RTSP etc.


GStreamer pipeline and product
------------------------------
Seems like there are several types of different level of abstraction for 
gstreamer, and I will need to pipe some of them. Also, 
there are some programs I will have to run to diagnose the system where the 
script will be running.

### Tools
I will be using the following tools:

 - v4l2-ctl: gives me information about the webcam.
 - gst-inspect: inspects what is installed and the properties of the 
 installed stuff.
 - gst-launch: launches a pipeline. Usually simple, and will be eventually 
 too limited. 

### The webcam
I have learnt about how to know about the webcam, 
`v4l2-ctl --list-formats-ext` provides information about the webcam  and all 
the formats it supports. Example outputs in data/webcams.txt. Three outputs 
from different computers have been merged there.

I suppose, but for the "Index" field, the output could be from any of the 
webcams. The format is very easy to read, and parsing it shouldn't be a problem.

### The source
I have to decide which quality I do need for video streaming. Tests need to be
done to decide quality over fps if needed.

I can recode all the streams through a pipeline if needed, but I can't improve
the quality once selected without switching the cam, introducing a gap in the
stream.

Therefore, samples are needed from all the possibilities. The fps/quality ratio
is totally related to the bandwidth available.
H.264-SVC or H.265 scalable.

Also, must be taken into account that I must belong at least to the groups
audio for audio and video for video.

### The stream
Imagining that we have all the gstreamer beginning pipeline convered, I would
still need to have the best transport streaming. I need to determine the protocol
to use.

The codec and the container are easier to setup because I just need the one
that better performance has. Specifically, VP9 as container and H264 as video
codec. I still need to figure out the best protocol.

If I want sync, I would need to use RTP, RTSP or UDP itself, mainly because
I wouldn't be able to discard packets if using one of the other protocols.


### The encryption
It's quite obvious that I would need some kind of openssl implementation for using
it. If I encrypt everything I wouldn't be able to discard those packets too because
that would mean that I wouldn't be able to read them.

Another option that has just come up to my mind is to use IPsec. This IPSec thing
would allow me not to think of the real encrytion, as I would just need to
configure that link using IPSec.

It's true that for such sort of script, that uses IPSec, I would need CAP_NET_RAW
capability, so that wouldn't ease the usability of this script.

Trying to achieve such usability means that I need to make it easy to use, so that
is a no go. I would need to use openssl, and in a future, be able to load it on
demand.

### The reception
In the receptor, I need to implement the possible video saving and the visualizer,
together with all the reverse pipeline.
