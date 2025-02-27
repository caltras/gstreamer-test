# gstreamer-test

## sending

gst-launch-1.0 osxaudiosrc ! audioconvert ! audioresample ! opusenc bitrate=64000 \
    ! rtpopuspay ! udpsink host=10.0.0.77 port=5004


## receiving

gst-launch-1.0 -v udpsrc port=5004 caps="application/x-rtp,media=(string)audio,clock-rate=(int)48000,encoding-name=(string)OPUS" \
    ! rtpopusdepay ! opusdec ! audioconvert ! autoaudiosink




## RECEIVE AUDIO FROM THE REMOTE OPERATOR
gst-launch-1.0 -v tcpserversrc host=(internal ip address of the home based computer) port=3000  ! gdpdepay !  rtpopusdepay ! opusdec plc=true ! audioconvert ! audioresample ! jackaudiosink sync=false

## TRANSMIT AUDIO TO THE REMOTE OPERATOR
gst-launch-1.0 -v jackaudiosrc ! audioconvert ! audioresample ! queue !  opusenc bitrate=256000 frame-size=2.5   ! rtpopuspay ! gdppay ! queue ! tcpserversink host=(internal ip address of home based computer) port=4000
