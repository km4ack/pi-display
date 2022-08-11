# Pi-Display

This project can be used to display information on a monitor using the chromium web browser. 
It will rotate through the links/files that you provide. HTML, PDF, JPG, PNG, PDF, MP4
are all supported. The project comes with sample files contained in the files directory.

# Installation

```
cd ~
git clone https://github.com/km4ack/pi-display.git
```

# Run the application

To run the application

```
~/pi-display/./pi-display
```

The script will run in a loop. After all of the files are displayed, chromium closes,
reopens, and displays the files again. To exit the script, `use ctrl+x` in the terminal
window where you stated the script.

# Add files to display

Two things must be done to add a new file into the rotation. First, place a copy of 
the file into ~/pi-display/files Next, add the file name to the links file. The initial
contents of the links file are:

```
DYK2.jpg,5
test.pdf,5
DYK1.jpg,5
weather.txt,5
radar.png,5
DYK3.jpg,5
news.txt,5
DYK4.jpg,5
test.html,5
https://google.com,5
```

Each file has to be included on a new line. The line begins with the file name followed
by a ",". After the "," a number must be added. This number tells the script how long to
display the page (in seconds) for that file.

# Remove a file from the display

To remove a file from the display, simply delete the line from the links file. Be sure
not to leave blank lines in the links file. Removing the file from the files directory
is optional.

# Kiosk Mode

If you would like to run the browser in Kiosk mode, open the pi-display script in a text
editor. Look for this line:

`KIOSK=OFF`

and change it to

`KIOSK=ON`
