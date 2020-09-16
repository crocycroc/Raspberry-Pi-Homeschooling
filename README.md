 
# About

This is a repository to keep track of all the patches that were required to get my child's Raspberry Pi 4 4GB model to work with the various platforms for her homeschooling.

## Webcam

Most modern USB webcams that I have tested appear to work on the Raspberry out of the box. Simply plug it in and that should be it.



## Microsoft Teams Support

To get Microsoft teams to work on the Raspberry Pi I needed to use the ventz-media-pi script

https://blog.vpetkov.net/2020/03/30/raspberry-pi-netflix-one-line-easy-install-along-with-hulu-amazon-prime-disney-plus-hbo-spotify-pandora-and-many-others/

Using the commands as follows will create a new instance of Chromium (Media Edition) in you start menu which will work with Microsoft teams.

```
curl -fsSL https://pi.vpetkov.net -o ventz-media-pi
sh ventz-media-pi
```

## Microsoft font Support

Pretty much a requriement for all Linux installs.

Running the following command on the Raspberry Pi will install the Microsoft fonts.

```
sudo apt install ttf-mscorefonts-installer
```

## Seesaw

Seesaw is an online educational platform that tends to have very bad error messages.

One issue you might run into is when you child tries to record audio you might get an error about the microphone being in use in another tab. This is incorrect the actual issue maybe that a microphone input has not been selected from the audio mixer tool on your Raspberry Pi. Just right click on the volume icon on the Pi and make sure to select and Input device from the list.

Another issue you might have is if your school using emoji graphics for the work sheets. These will display in browser as square boxes when the font's lack those symbols. You will need to install a font pack that includes support for colored emojis.

Found the following script from an article here https://www.raspberrypi.org/forums/viewtopic.php?t=253484 that will allow you to download the required fonts from public sources that will give chromium the ability to render such characters. Please note that you may need to close and restart chromium for the fonts to load in properly.

```
mkdir ~/tmp
cd tmp
wget https://fontsdata.com/zipdown-segoeuiemoji-132714.htm 
wget https://noto-website.storage.googleapis.com/pkgs/NotoColorEmoji-unhinted.zip
mv zipdown-segoeuiemoji-132714.htm segoeuiemoji.zip
unzip segoeuiemoji.zip
unzip NotoColorEmoji-unhinted.zip
mkdir /home/pi/.fonts &>/dev/null
mv seguiemj.ttf "/home/pi/.fonts/Segoe UI.ttf"
mv NotoColorEmoji.ttf "/home/pi/.fonts/Noto Color Emoji.ttf"
fc-cache -f -v &>/dev/null
rm -r ~/tmp
cd
```
