# Pi-Display

This project can be used to display information on a monitor using the chromium web browser. 
It will rotate through the links/files that you provide. HTML, PDF, JPG, PNG, PDF, MP4
are all supported. The project comes with sample files contained in the files directory.

# Video

[![IMAGE ALT TEXT](http://img.youtube.com/vi/BB6ZqO5Vkyg/0.jpg)](https://www.youtube.com/watch?v=BB6ZqO5Vkyg "Pi Display Overview")

[![IMAGE ALT TEXT](http://img.youtube.com/vi/5O3nXKQn51A/0.jpg)](https://www.youtube.com/watch?v=5O3nXKQn51A "Pi Display Install & Overview")

# Installation

Run the command below to install on your Debian system.

```
git clone https://github.com/km4ack/pi-display.git $HOME/pi-display
```

# Start the application

Use the command below to start the application.

```
~/pi-display/./pi-display
```

The script will run in a loop. After all of the files are displayed, chromium closes,
reopens, and displays the files again. To exit the script, use `ctrl+c` in the terminal
window where you stated the script.

# Add files to display

Two things must be done to add a new file into the rotation. First, place a copy of 
the file into ~/pi-display/files/ Next, add the file name to the links file. The initial
contents of the links file are:

```
/pota/POTA6.jpg,5
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
by a ",". After the "," a number must be added. This number tells the script how long (in seconds) to
display the page for that file. Notice the first line above `/pota/POTA6.jpg,5` You will find a pota 
subdirectory under files. 

# Remove a file from the display

To remove a file from the display, simply delete the line from the links file. Be sure
not to leave blank lines in the links file. Removing the file from the files directory
is optional.

# Weather-report

This script will help you generate a weather report and output the results as a HTML file
that is copied to the pi-display files for display. To run the script, use the following command

```
~/pi-display/./weather-report
```

# Markdown

This script will help you generate a quick web page using the markdown language. It also saves your work to ~/pi-display/tmp/ so that you
can edit the file(s) in the future with this script. If you aren't familiar with the simplicity of markdown, checkout [this page](https://www.markdownguide.org/cheat-sheet)
To run, use the following command

```
~/pi-display/./markdown
```
# auto-screenshot

This script is included but designed to be run on another computer in conjunction with pi-display. Once copied to the other machine
and started, it will create a web server and capture screenshot at the interval set (60 second default) in the script.
This screenshot can then be pulled into the pi-display. I use it to screen shot an APRS digipeater map
than can then be viewed on the pi-display machine. Note:python3 is required for this script to work.

# Import

An import script is included for importing multiple files as once and automatically adding them
to the slideshow. This is especially helpful when importing many images. An import directory must be specified
as the first argument. Example:

```
./import /path/to/import/
```
The time set to display each slide is applied to all of the
imported files but can be modified after the import in the ~/pi-display/links file.

# Ideas for things to run on the Pi Display

- Did you Know series (included with Pi Display)
- Solar Forecast
- Weather Forecast
- Weather Warnings
- Propagation Prediction Images (VOACAP)
- FLMSG HTML Pages
- Images of the Day
- APRS Map (pulled from digipeater)
- Announcements (next club meeting, meet ups, etc)
- FD/WFD Schedule
- POTA Slides (included with Pi Display)
- Station Capabilities
- Local Repeater Info
- Club Simplex Frequency 
- Info to support event
-- Number of riders/runners to finish
-- Location of lead rider/runner
-- Location of last rider/runner
-- Net Control Frequency

# Kiosk Mode

If you would like to run the browser in Kiosk mode, open the pi-display script in a text
editor. Look for this line:

`KIOSK=OFF`

and change it to

`KIOSK=ON`
