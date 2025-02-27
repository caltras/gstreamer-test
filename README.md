# gstreamer-test

## sending

gst-launch-1.0 osxaudiosrc ! audioconvert ! audioresample ! opusenc bitrate=64000 \
    ! rtpopuspay ! udpsink host=10.0.0.77 port=5004


## receiving

gst-launch-1.0 -v udpsrc port=5004 caps="application/x-rtp,media=(string)audio,clock-rate=(int)48000,encoding-name=(string)OPUS" \
    ! rtpopusdepay ! opusdec ! audioconvert ! autoaudiosink


