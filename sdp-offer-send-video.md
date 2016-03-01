# SDP offer with single video


## Scene

A WebRTC 1.0 browser is willing to send its webcam video without receiving any audio/video from the remote peer:

```js
// Request webcam access
navigator.mediaDevices.getUserMedia({ audio: false, video: true })
    .then(function(stream)
    {
        // Create a RTCPeerConnection
        var pc = new RTCPeerConnection({ iceServers: [] });

        // Add our local MediaStream
        pc.addStream(stream);

        // Create a SDP offer without audio m= line
        pc.createOffer({ offerToReceiveAudio: 0 })
            .then(function(desc)
            {
                console.log('SDP offer:\n%s', desc.sdp);
            });
    });
```

The generated SDP offers looks as follows (Chrome M48):

```
v=0
o=- 8007099234039195135 2 IN IP4 127.0.0.1
s=-
t=0 0
a=group:BUNDLE video
a=msid-semantic: WMS 5FycVqBH7W4UNDJJuzzikeHgN97FA7YZLAGJ
m=video 54336 UDP/TLS/RTP/SAVPF 100 101 116 117 96
c=IN IP4 192.168.56.1
a=rtcp:65452 IN IP4 192.168.56.1
a=candidate:896251694 1 udp 2122262783 a:b:c:d::1 61465 typ host generation 0
a=candidate:2999745851 1 udp 2122194687 192.168.56.1 54336 typ host generation 0
a=candidate:2896278100 1 udp 2122129151 192.168.1.36 49979 typ host generation 0
a=candidate:896251694 2 udp 2122262782 a:b:c:d::1 49980 typ host generation 0
a=candidate:2999745851 2 udp 2122194686 192.168.56.1 65452 typ host generation 0
a=candidate:2896278100 2 udp 2122129150 192.168.1.36 54301 typ host generation 0
a=candidate:2078821342 1 tcp 1518283007 a:b:c:d::1 0 typ host tcptype active generation 0
a=candidate:4233069003 1 tcp 1518214911 192.168.56.1 0 typ host tcptype active generation 0
a=candidate:3793899172 1 tcp 1518149375 192.168.1.36 0 typ host tcptype active generation 0
a=candidate:2078821342 2 tcp 1518283006 a:b:c:d::1 0 typ host tcptype active generation 0
a=candidate:4233069003 2 tcp 1518214910 192.168.56.1 0 typ host tcptype active generation 0
a=candidate:3793899172 2 tcp 1518149374 192.168.1.36 0 typ host tcptype active generation 0
a=ice-ufrag:besXu9nd9xe37Z3f
a=ice-pwd:SB+/98Xf8fAGwxwIUT0kpOv2
a=fingerprint:sha-256 0D:46:D5:9F:BE:E2:3A:5A:65:5F:CD:31:F9:39:D8:18:C4:74:A8:B0:C5:05:DA:B5:0F:39:29:01:7E:1F:26:CD
a=setup:actpass
a=mid:video
a=extmap:2 urn:ietf:params:rtp-hdrext:toffset
a=extmap:3 http://www.webrtc.org/experiments/rtp-hdrext/abs-send-time
a=extmap:4 urn:3gpp:video-orientation
a=sendonly
a=rtcp-mux
a=rtpmap:100 VP8/90000
a=rtcp-fb:100 ccm fir
a=rtcp-fb:100 nack
a=rtcp-fb:100 nack pli
a=rtcp-fb:100 goog-remb
a=rtpmap:101 VP9/90000
a=rtcp-fb:101 ccm fir
a=rtcp-fb:101 nack
a=rtcp-fb:101 nack pli
a=rtcp-fb:101 goog-remb
a=rtpmap:116 red/90000
a=rtpmap:117 ulpfec/90000
a=rtpmap:96 rtx/90000
a=fmtp:96 apt=100
a=ssrc-group:FID 19936785 1592093127
a=ssrc:19936785 cname:30uugWU8uBaMClU0
a=ssrc:19936785 msid:5FycVqBH7W4UNDJJuzzikeHgN97FA7YZLAGJ e293cdb4-15d9-4824-be8b-f4d93fe8a96f
a=ssrc:19936785 mslabel:5FycVqBH7W4UNDJJuzzikeHgN97FA7YZLAGJ
a=ssrc:19936785 label:e293cdb4-15d9-4824-be8b-f4d93fe8a96f
a=ssrc:1592093127 cname:30uugWU8uBaMClU0
a=ssrc:1592093127 msid:5FycVqBH7W4UNDJJuzzikeHgN97FA7YZLAGJ e293cdb4-15d9-4824-be8b-f4d93fe8a96f
a=ssrc:1592093127 mslabel:5FycVqBH7W4UNDJJuzzikeHgN97FA7YZLAGJ
a=ssrc:1592093127 label:e293cdb4-15d9-4824-be8b-f4d93fe8a96f
```
