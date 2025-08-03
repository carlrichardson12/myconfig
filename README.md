sudo docker rm -f cam-stream


sudo modprobe bcm2835-v4l2  # Enable camera as /dev/video0



sudo docker run -d \
  --name cam-stream \
  --privileged \
  -v /dev/video0:/dev/video0 \
  -p 8080:8080 \
  patsoffice/mjpg-streamer


docker rm -f cam-stream 2>/dev/null

docker run -d \
  --name cam-stream \
  --privileged \
  -v /dev/video0:/dev/video0 \
  -p 8080:8080 \
  patsoffice/mjpg-streamer
