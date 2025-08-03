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



sudo apt update
sudo apt install v4l2loopback-utils
sudo modprobe v4l2loopback devices=1 video_nr=10 card_label="VirtualCam" exclusive_caps=1
ls /dev/video*
sudo apt install ffmpeg
libcamera-vid -t 0 --inline --width 640 --height 480 --framerate 25 --codec yuv420 --nopreview | \
ffmpeg -f rawvideo -pix_fmt yuv420p -s 640x480 -i - -f v4l2 /dev/video10

sudo docker rm -f cam-stream

sudo docker run -d \
  --name cam-stream \
  --privileged \
  -v /dev/video10:/dev/video0 \
  -p 8080:8080 \
  patsoffice/mjpg-streamer

  http://10.0.0.96:8080/?action=stream



sudo docker rm -f cam-stream

sudo docker run -d \
  --name cam-stream \
  --privileged \
  -v /dev/video10:/dev/video0 \
  -p 8080:8080 \
  patsoffice/mjpg-streamer


sudo apt update
sudo apt install raspberrypi-kernel-headers build-essential git dkms
uname -r
git clone https://github.com/umlaeute/v4l2loopback.git
cd v4l2loopback
make
sudo make install
sudo modprobe v4l2loopback video_nr=10 card_label="VirtualCam" exclusive_caps=1

ls -l /dev/video10
echo "v4l2loopback video_nr=10 card_label=VirtualCam exclusive_caps=1" | sudo tee /etc/modules-load.d/v4l2loopback.conf


#!/bin/bash

set -e

echo "🔧 Updating system and installing dependencies..."
sudo apt update
sudo apt install -y git build-essential raspberrypi-kernel-headers dkms

echo "📁 Cloning v4l2loopback repo..."
git clone https://github.com/umlaeute/v4l2loopback.git /tmp/v4l2loopback
cd /tmp/v4l2loopback

echo "🛠️ Building v4l2loopback kernel module..."
make

echo "📦 Installing the module..."
sudo make install

echo "📂 Creating autoload config..."
echo "v4l2loopback video_nr=10 card_label=VirtualCam exclusive_caps=1" | \
  sudo tee /etc/modules-load.d/v4l2loopback.conf > /dev/null

echo "📥 Loading v4l2loopback module now..."
sudo modprobe v4l2loopback video_nr=10 card_label="VirtualCam" exclusive_caps=1

echo "✅ Done!"
echo "🎥 Checking for /dev/video10..."

if [ -e /dev/video10 ]; then
  echo "🎉 Success: /dev/video10 is ready."
else
  echo "⚠️ Warning: /dev/video10 not found. Reboot may be required."
fi



