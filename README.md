# pi-timelapse
Time lapse photography using raspberry pis

Description: This project tries to deliver a unique user experience everytime a user navigates to the URL. I don't know if unique is the right word. Basically, hitting the URL should provide different visuals every time.

Background: I originally did this project when I lived in Seattle. I didn't bother to document any of it because documentation is for losers. So, when it stopped working suddenly, I had no clue how to fix it. This will hopefully fix that.

Tech overview:
Picture taken by pi zero every 15 minutes and written to mounted drive on pi 5 -> Pi 5 processes picture: Creates 2 versions, "thumbnail" and "web" sized -> Pi 5 uploads to webserver for happy action fun time -> User interacts with page and gets happy action fun time view of pictures

## Assumptions:
 1. You have a website (or an internal network).
 2. You have some money.
 3. You have some free time.
 4. You are interested in learning stuff.
 5. You are ok with typing 'sudo apt get' a lot of times and you don't really understand why you are doing it.
 6. You use AI. These steps will not include using AI, but I used AI (chatgpt) extensively in this process. My initial build used whatever I could find on the internet which was that awkward period where all the search engines pointed you to references that paid them money (aka, not necessarily the best sources) and AI either didn't exist or was just a novelty. AI will confidently give you incorrect information, but it will not be an a-hole and tell you to read other posts that answer the same question (I'm looking at you stackoverflow). If you get stuck, maybe try pinging an AI thingy rather than searching on the internet. At a minimum, the AI will be nice while giving you bad information rather than being a jerk about it.

## Hardware list, costs (at the time of purchase), link, notes:
| item | cost | link | notes |
|----|------|----|----|
| Raspberry Pi Zero 2 W | $54.99| https://www.amazon.com/dp/B09M1PS35R?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1 | I bricked my pi zero w (don't plug in a pi while it is sitting on metal), so I bought a newer model. |
| Raspberry Pi Camera module | $29.95 | https://www.amazon.com/dp/B01ER2SKFS?ref=ppx_yo2ov_dt_b_fed_asin_title | There might be more suitable models. Also, the camera ribbon SUUUUUUCKS |
| Raspberry Pi 5 | $179.99 | https://www.amazon.com/dp/B0CRSPKPNG?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1 | This guy does picture processsing + is my media player (kodi). My initial build used a pi 4 (sans kodi). |

There are quality of life items I bought in addition to these items. The list above is bare bones. For example, I built a ghetto NAS to hold my media and the pictures, but you can probably get away with doing a sync to your website and leverage the onboard storage of the pi used to process the pictures. Just keep storage in mind with your build. Keep in mind placement of your camera. Keep in mind putting a shroud around the camera module.

## Setting up the Pi Zero:
1. Set up your SD card using Raspberry Pi Imager (https://downloads.raspberrypi.com/imager/imager_latest.exe).
2. The device is a Raspberry Pi Zero 2 W and you'll want the Raspberry Pi OS (32-bit) with Desktop.
3. Make sure you select the SD card.
4. Use the following settings (I'm doing this from memory - sorry).
 * a. hostname: pick something memorable. I used piCamera.
 * b. enable SSH: yes - SSH will allow you to remote in with a command line, which is really nice because then you don't have to connect a monitor and a mouse/keyboard.
 * c. username: pick one and make sure you remember it.
 * d. password: pick one and make sure you remember it.
 * e. WiFi SSID/password: set that up so you have connectivity once it boots.
 * f. Raspberry Connect - I did not enable this, but maybe I should have?
5. Connect the camera to the pi zero.
6. Insert the SD card.
7. MAKE SURE YOU DO NOT HAVE THE PI ZERO SITTING DIRECTLY ON A METAL SURFACE. Power it on.
8. While it's booting, open a command prompt on your windows machine and spam "ping hostname". Once you get a response, you should be good to go in connecting via SSH (next step). If you installed Raspberry Connect, I suppose you could do that rather than SSH.
9. SSH into the pi zero. Open a command prompt and type "ssh hostname". You shouldn't need to put in the username since there should only be one, but you could probably do something like "ssh username@hostname". At some point, you'll get a warning about the authenticity of the host and how it can't be established. Type yes and hit enter.
10. Enter the password.
11. If you mess up the password, enter it again.* 
12. Once in, enter the following commands to perform some kind of weird magic that seems pretty important:
 * a. sudo apt update
 * b. sudo apt full-upgrade -y
 * c. sudo reboot
13. In your command prompt, spam "ping hostname" until it responds then ssh in again.
14. Once you're back in, enable VNC so you can remote into the desktop. Note: this isn't necessary, but I'm a n00b, and you will need to pry my desktop from my cold dead hands. Note-note: You can probably do this via the command line, but see the previous note.
 * a. Type: sudo raspi-config
 * b. Use up/down arrows to select Interface Options and hit enter.
 * c. Use up/down arrows to select VNC and hit enter.
 * d. At "Would you like the VNC Server to be enabled?", highlight <Yes> and then hit enter.
 * e. Type: sudo reboot
15. While it's rebooting, download RealVNC Viewer for windows (https://downloads.realvnc.com/download/file/viewer.files/VNC-Viewer-7.15.1-Windows.exe?lai_vid=eebXdjBBQIm6&lai_sr=0-4&lai_sl=l). Note: You can use mstsc for windows, but I'm not sure if you can reference the pi using the hostname. This is what I used the first time I did it, but I logged in using a static IP which I configured for the old infrastructure. If you go that route instead of realVNC, you could try connecting via hostname.local. I don't think this'll work unless you install something that will do fancy pants DNS stuff (whatever that is), but it's worth a shot. Update: I tested it without the fancy pants DNS stuff and it did not work. So, realVNC it is.
