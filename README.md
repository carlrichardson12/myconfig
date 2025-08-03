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


 hostname -I 
10.0.0.96 172.17.0.1 169.254.5.66 2601:c4:4480:c890::3ec2 2601:c4:4480:c890:e1c4:60a2:b9c6:3da5 
