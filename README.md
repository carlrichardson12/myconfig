sudo docker rm -f cam-stream


sudo modprobe bcm2835-v4l2  # Enable camera as /dev/video0



sudo docker run -d \
  --name cam-stream \
  --privileged \
  -v /dev/video0:/dev/video0 \
  -p 8080:8080 \
  patsoffice/mjpg-streamer


bcm2835-codec-decode (platform:bcm2835-codec):
	/dev/video10
	/dev/video11
	/dev/video12
	/dev/video18
	/dev/video31
	/dev/media3

bcm2835-isp (platform:bcm2835-isp):
	/dev/video13
	/dev/video14
	/dev/video15
	/dev/video16
	/dev/video20
	/dev/video21
	/dev/video22
	/dev/video23
	/dev/media0
	/dev/media1

unicam (platform:fe801000.csi):
	/dev/video0
	/dev/media2
