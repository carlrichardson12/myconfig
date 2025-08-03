docker run -d \
  --name cam-stream \
  --restart unless-stopped \
  --device /dev/video0 \
  -p 8080:8080 \
  -v /dev/shm:/dev/shm \
  lsioarmhf/mjpg-streamer


  docker run -d \
  --name cam-stream \
  --privileged \
  -v /dev/video0:/dev/video0 \
  -p 8080:8080 \
  -e RESOLUTION="1280x720" \
  -e FPS="15" \
  undermozes/mjpg-streamer




  sudo apt install v4l2loopback-dkms
  

  sudo modprobe v4l2loopback video_nr=0 card_label="VirtualCam" exclusive_caps=1


libcamera-vid -t 0 --width 640 --height 480 --framerate 25 --codec yuv420 --output /dev/video0
