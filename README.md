# Live-Streaming-Video-using-Rasperry-Pi-3
This project demonstrates step by step:  How to use raspberry pi camera for live streaming over web using "MJPG Streamer"


Open your terminal and perform the following action:

Go to command line and write:

sudo raspi-config 


Enable the camera as shown in the video

and then return to command line and perform the following steps:


1. Install dependecies

sudo apt-get install libjpeg8-dev imagemagick libv4l-dev


2. Add link:

sudo ln -s /usr/include/linux/videodev2.h /usr/include/linux/videodev.h


3. Download MJPG Streamer


wget http://sourceforge.net/code-snapshots/svn/m/mj/mjpg-streamer/code/mjpg-streamer-code-182.zip

4. Unzip the file:
unzip mjpg-streamer-code-182.zip


5. Build MJPG streamer:


cd mjpg-streamer-code-182/mjpg-streamer


make mjpg_streamer input_file.so output_http.so


6. Install MJPG-Streamer

sudo cp mjpg_streamer /usr/local/bin
sudo cp output_http.so input_file.so /usr/local/lib/
sudo cp -R www /usr/local/www


7. Start the Camera

mkdir /tmp/stream

raspistill --nopreview -w 640 -h 480 -q 5 -o /tmp/stream/pic.jpg -tl 100 -t 9999999 -th 0:0:0 &


8. Start the MJPG streamer:


LD_LIBRARY_PATH=/usr/local/lib mjpg_streamer -i "input_file.so -f /tmp/stream -n pic.jpg" -o "output_http.so -w /usr/local/www -c username:password"


Now go to the IP address of your connection:



or If you want to see the stream on Raspberry Pi:

http://localhost:8080/


Give User ID and password and enjoy it !

CHECK THE VIDEO FOR STEP BY STEP INSTALLATION:

https://www.youtube.com/watch?v=aJbCyAU2270&feature=youtu.be
