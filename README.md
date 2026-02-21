# pi-timelapse
Time lapse photography using raspberry pis

Description: This project tries to deliver a unique user experience everytime a user navigates to the URL. I don't know if unique is the right word. Basically, hitting the URL should provide different visuals every time.

Background: I originally did this project when I lived in Seattle. I didn't bother to document any of it because documentation is for losers. So, when it stopped working suddenly, I had no clue how to fix it. This will hopefully fix that.

Tech overview:
Picture taken by pi zero every 15 minutes and written to mounted drive on pi 5 -> Pi 5 processes picture: Creates 2 versions, "thumbnail" and "web" sized -> Pi 5 uploads to webserver for happy action fun time -> User interacts with page and gets happy action fun time view of pictures

Assumptions:
 1. You have a website (or an internal network).
 2. You have some money.
 3. You have some free time.
 4. You are interested in learning stuff.
 5. You are ok with typing 'sudo apt get' a lot of times and you don't really understand why you are doing it.
 6. You use AI. These steps will not include using AI, but I used AI (chatgpt) extensively in this process. My initial build used whatever I could find on the internet which was that awkward period where all the search engines pointed you to references that paid them money (aka, not necessarily the best sources) and AI either didn't exist or was just a novelty. AI will confidently give you incorrect information, but it will not be an a-hole and tell you to read other posts that answer the same question (I'm looking at you stackoverflow). If you get stuck, maybe try pinging an AI thingy rather than searching on the internet. At a minimum, the AI will be nice while giving you bad information rather than being a jerk about it.

Hardware list, costs (at the time of purchase), link, notes:
item                        cost      link                                                                          notes
Raspberry Pi Zero 2 W       $54.99    https://www.amazon.com/dp/B09M1PS35R?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1  I bricked my pi zero w (don't plug in a pi while it is sitting on metal), so I bought a newer model. 
Raspberry Pi Camera module  $29.95    https://www.amazon.com/dp/B01ER2SKFS?ref=ppx_yo2ov_dt_b_fed_asin_title        There might be more suitable models. Also, the camera ribbon SUUUUUUCKS
Raspberry Pi 5              $179.99   https://www.amazon.com/dp/B0CRSPKPNG?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1  This guy does picture processsing + is my media player (kodi). My initial build used a pi 4 (sans kodi).

There are quality of life items I bought in addition to these items. The list above is bare bones. For example, I built a ghetto NAS to hold my media and the pictures, but you can probably get away with doing a sync to your website and leverage the onboard storage of the pi used to process the pictures. Just keep storage in mind with your build. Keep in mind placement of your camera. Keep in mind putting a shroud around the camera module.

Setting up the Pi Zero:
1. Format an appropriately sized sd card with the appropriate os for the pi zero. I'm not a linux user, so I opted for a gui (graphical user interface - I'm going to spell it out unlike the linux crowd that just assumes you know [and care] what sudo apt get actually does) because I like to have a desktop when I remote into the "computer"... Even though I mostly used the command line interface to execute commands (the equivalent of windows key + r -> cmd) once on the desktop. But I digress.
2. 
