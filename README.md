# gstreamer-test

## sending

gst-launch-1.0 -v udpsrc port=5004 \
    ! audio/x-raw,format=S16LE,rate=48000,channels=2 \
    ! audioconvert ! autoaudiosink


## receiving

gst-launch-1.0 -v udpsrc port=5004 caps="application/x-rtp,media=(string)audio,clock-rate=(int)48000,encoding-name=(string)OPUS" \
    ! rtpopusdepay ! opusdec ! audioconvert ! autoaudiosink

