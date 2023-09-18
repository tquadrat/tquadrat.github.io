# The Raspberry Camera

## Taking photos with the Raspberry Camera

### The `raspistill` Camera App

Runs the camera for a specific time, and takes a JPEG capture at the end if requested.

Usage: `raspistill [options]`

#### Image parameter commands

 - `-q`, `--quality` – Sets the JPRG quality within a range from 0 to 100
 - `-r`, `--raw` – Adds raw bayer data to the JPEG metadata
 - `-l <filename>`, `--latest <filename>` – Links the latest complete image to  the given filename
 - `-t <delay>`, `--timeout <delay>` – The time (in ms) before taking the picture and terminating (if not specified, it is set to 5s)
 - `-th {<x>:<y>:<quality> | none}`, `--thumb {<x>:<y>:<quality> | none}` – Sets the thumbnail parameters
 - `-d`, `--demo` –	Runs a demo mode (cycles through the range of camera options, without a capture)
 - `-e {jpg | bmp | gif | png}`, `--encoding {jpg | bmp | gif | png}` – The Encoding to use for the output file
 - `-x {<key>=<value> | none}`, `--exif {<key>=<value> | none}`	– EXIF tag to apply to the captures
 - `-tl`, `--timelapse` – Timelapse mode; takes a picture every `<t>` ms. %d == frame number in the output file name (Try: `-o img_%04d.jpg`)
 - `-fp`, `--fullpreview`	– Runs the preview using the still capture resolution (may reduce preview framerate)
 - `-k`, `--keypress`	– Waits between captures for a `ENTER`, `X` then `ENTER` to exit the program
 - `-s`, `--signal`	– Waits between captures for a `SIGUSR1` or `SIGUSR2` from another process
 - `-g`, `--gl`	– Draws the preview to texture instead of using the video render component
 - `-gc`, `--glcapture`	– Captures the GL frame-buffer instead of the camera image
 - `-bm`, `--burst`	– Enable 'burst capture mode'
 - `-dt`, `--datetime`	– Replaces the output pattern `%d` with DateTime in the format "MonthDayHourMinSec"
 - `-ts`, `--timestamp` – Replaces the output pattern `%d` with  the Unix timestamp (seconds since 1970-01-01T00:00:00 UTC)
 - `-fs`, `--framestart`	– Sets the starting frame number to the output pattern `%d`
 - `-rs [<interval>]`, `--restart [<interval>]`	– Sets the JPEG Restart interval (default of 0 for none)

#### GL parameter commands

 - `-gs {square | teapot | mirror | yuv | sobel | vcsm_square}`, `--glscene {square | teapot | mirror | yuv | sobel | vcsm_square}` – GL scene
 - `-gw <x>,<y>,<w>,<h>`, `--glwin <x>,<y>,<w>,<h>`	– GL window settings

#### Common Settings commands

-?, --help	: This help information
-w, --width	: Set image width <size>
-h, --height	: Set image height <size>
-o, --output	: Output filename <filename> (to write to stdout, use '-o -'). If not specified, no file is saved
-v, --verbose	: Output verbose information during run
-cs, --camselect	: Select camera <number>. Default 0
-md, --mode	: Force sensor mode. 0=auto. See docs for other modes available
-gps, --gpsdexif	: Apply real-time GPS information to output (e.g. EXIF in JPG, annotation in video (requires libgps.so.23)

#### Preview parameter commands

 - `-p <x>,<y>,<w>,<h>`, `--preview <x>,<y>,<w>,<h>` – Preview window settings
 - `-f`, `--fullscreen`	– Fullscreen preview mode
 - `-op <opacity>`, `--opacity <opacity>`	– Sets the preview window opacity (0-255)
 - `-n`, `--nopreview`	– Do not display a preview window
 - `-dn <display>`, `--dispnum <display>` – Display on which to display the preview window (dispmanx/tvservice numbering)

Image parameter commands

-sh, --sharpness	: Set image sharpness (-100 to 100)
-co, --contrast	: Set image contrast (-100 to 100)
-br, --brightness	: Set image brightness (0 to 100)
-sa, --saturation	: Set image saturation (-100 to 100)
-ISO, --ISO	: Set capture ISO
-vs, --vstab	: Turn on video stabilisation
-ev, --ev	: Set EV compensation - steps of 1/6 stop
-ex, --exposure	: Set exposure mode (see Notes)
-fli, --flicker	: Set flicker avoid mode (see Notes)
-awb, --awb	: Set AWB mode (see Notes)
-ifx, --imxfx	: Set image effect (see Notes)
-cfx, --colfx	: Set colour effect (U:V)
-mm, --metering	: Set metering mode (see Notes)
-rot, --rotation	: Set image rotation (0, 90, 180, or 270)
-hf, --hflip	: Set horizontal flip
-vf, --vflip	: Set vertical flip
-roi, --roi	: Set region of interest (x,y,w,d as normalised coordinates [0.0-1.0])
-ss, --shutter	: Set shutter speed in microseconds
-awbg, --awbgains	: Set AWB gains - AWB mode must be off
-drc, --drc	: Set DRC Level (see Notes)
-st, --stats	: Force recomputation of statistics on stills capture pass
-a, --annotate	: Enable/Set annotate flags or text
-3d, --stereo	: Select stereoscopic mode
-dec, --decimate	: Half width/height of stereo image
-3dswap, --3dswap	: Swap camera order for stereoscopic
-ae, --annotateex	: Set extra annotation parameters (text size, text colour(hex YUV), bg colour(hex YUV), justify, x, y)
-ag, --analoggain	: Set the analog gain (floating point)
-dg, --digitalgain	: Set the digital gain (floating point)
-set, --settings	: Retrieve camera settings and write to stdout
-fw, --focus	: Draw a window with the focus FoM value on the image.


Notes

Exposure mode options :
off,auto,night,nightpreview,backlight,spotlight,sports,snow,beach,verylong,fixedfps,antishake,fireworks

Flicker avoid mode options :
off,auto,50hz,60hz

AWB mode options :
off,auto,sun,cloud,shade,tungsten,fluorescent,incandescent,flash,horizon,greyworld

Image Effect mode options :
none,negative,solarise,sketch,denoise,emboss,oilpaint,hatch,gpen,pastel,watercolour,film,blur,saturation,colourswap,washedout,posterise,colourpoint,colourbalance,cartoon

Metering Mode options :
average,spot,backlit,matrix

Dynamic Range Compression (DRC) options :
off,low,med,high





Foto mit der Kamera aufnehmen:

$ raspistill -v -o <dateiname>

Hierbei wird ein Foto mit eine (standarmäßig eingestellten) Verzögerung von fünf Sekunden aufgenommen und als JPEG mit dem angegebenen Dateinamen gespeichert. Durch die Option -v werden zusätzlich noch einige Informationen auf der Konsole ausgegeben.

Verzögerung
----------
Der CCD-Chip der Kamera benötigt eine gewisse Zeit zur Auto-Justierung, so dass der default-Wert für die Verzögerung auf 5000 Millisekunden eingestellt ist. Durch Angabe der Option "-t <delay>" kann die Verzögerung auf den angegebenen Wert in Millisekunden verändert werden; sie kann bis auf eine Millisekunde verringert werden, darunter leidet allerdings die Gesamtqualität des Fotos deutlich, insbesondere bei den Farben und beim Kontrast. 700 bis 1000 Millisekunden scheinen ein guter Wert zu sein, um vernünftige Fotos zu machen.

Spiegeln der Aufnahme
---------------------
Je nachdem wie das Kamera-Modul verbaut und aufgestellt wurde, kann es sein, dass man die Aufnahmen spiegeln möchte.

Mit der Option "-hf" spiegelt man das Foto horizontal, während die Option "-vf" es vertikal spiegelt.

---
## Shooting Videos with the Raspberry Camera

### The `raspivid` Camera App

Displays camera output to the display, and optionally saves an H264 capture at requested bitrate.

Usage: `raspivid [options]`

#### Image parameter commands

-b, --bitrate	: Set bitrate. Use bits per second (e.g. 10MBits/s would be -b 10000000)
-t, --timeout	: Time (in ms) to capture for. If not specified, set to 5s. Zero to disable
 - `-d`, `--demo` –	Runs a demo mode (cycles through the range of camera options, without a capture)
-fps, --framerate	: Specify the frames per second to record
-e, --penc	: Display preview image *after* encoding (shows compression artifacts)
-g, --intra	: Specify the intra refresh period (key frame rate/GoP size). Zero to produce an initial I-frame and then just P-frames.
-pf, --profile	: Specify H264 profile to use for encoding
-td, --timed	: Cycle between capture and pause. -cycle on,off where on is record time and off is pause time in ms
-s, --signal	: Cycle between capture and pause on Signal
-k, --keypress	: Cycle between capture and pause on ENTER
-i, --initial	: Initial state. Use 'record' or 'pause'. Default 'record'
-qp, --qp	: Quantisation parameter. Use approximately 10-40. Default 0 (off)
-ih, --inline	: Insert inline headers (SPS, PPS) to stream
-sg, --segment	: Segment output file in to multiple files at specified interval <ms>
-wr, --wrap	: In segment mode, wrap any numbered filename back to 1 when reach number
-sn, --start	: In segment mode, start with specified segment number
-sp, --split	: In wait mode, create new output file for each start event
-c, --circular	: Run encoded data through circular buffer until triggered then save
-x, --vectors	: Output filename <filename> for inline motion vectors
-if, --irefresh	: Set intra refresh type
-fl, --flush	: Flush buffers in order to decrease latency
-pts, --save-pts	: Save Timestamps to file for mkvmerge
-cd, --codec	: Specify the codec to use - H264 (default) or MJPEG
-lev, --level	: Specify H264 level to use for encoding
-r, --raw	: Output filename <filename> for raw video
-rf, --raw-format	: Specify output format for raw video. Default is yuv
-l, --listen	: Listen on a TCP socket
-stm, --spstimings	: Add in h.264 sps timings
-sl, --slices	: Horizontal slices per frame. Default 1 (off)


H264 Profile options :
baseline,main,high

H264 Level options :
4,4.1,4.2

H264 Intra refresh options :
cyclic,adaptive,both,cyclicrows

Raw output format options :
yuv,rgb,gray

Raspivid allows output to a remote IPv4 host e.g. -o tcp://192.168.1.2:1234 or -o udp://192.168.1.2:1234
To listen on a TCP port (IPv4) and wait for an incoming connection use the -l option
e.g. raspivid -l -o tcp://0.0.0.0:3333 -> bind to all network interfaces,
raspivid -l -o tcp://192.168.1.1:3333 -> bind to a certain local IPv4 port

Common Settings commands

-?, --help	: This help information
-w, --width	: Set image width <size>
-h, --height	: Set image height <size>
-o, --output	: Output filename <filename> (to write to stdout, use '-o -'). If not specified, no file is saved
-v, --verbose	: Output verbose information during run
-cs, --camselect	: Select camera <number>. Default 0
-md, --mode	: Force sensor mode. 0=auto. See docs for other modes available
-gps, --gpsdexif	: Apply real-time GPS information to output (e.g. EXIF in JPG, annotation in video (requires libgps.so.23)

#### Preview parameter commands

 - `-p <x>,<y>,<w>,<h>`, `--preview <x>,<y>,<w>,<h>` – Preview window settings
 - `-f`, `--fullscreen`	– Fullscreen preview mode
 - `-op <opacity>`, `--opacity <opacity>`	– Sets the preview window opacity (0-255)
 - `-n`, `--nopreview`	– Do not display a preview window
 - `-dn <display>`, `--dispnum <display>` – Display on which to display the preview window (dispmanx/tvservice numbering)

Image parameter commands

-sh, --sharpness	: Set image sharpness (-100 to 100)
-co, --contrast	: Set image contrast (-100 to 100)
-br, --brightness	: Set image brightness (0 to 100)
-sa, --saturation	: Set image saturation (-100 to 100)
-ISO, --ISO	: Set capture ISO
-vs, --vstab	: Turn on video stabilisation
-ev, --ev	: Set EV compensation - steps of 1/6 stop
-ex, --exposure	: Set exposure mode (see Notes)
-fli, --flicker	: Set flicker avoid mode (see Notes)
-awb, --awb	: Set AWB mode (see Notes)
-ifx, --imxfx	: Set image effect (see Notes)
-cfx, --colfx	: Set colour effect (U:V)
-mm, --metering	: Set metering mode (see Notes)
-rot, --rotation	: Set image rotation (0, 90, 180, or 270)
-hf, --hflip	: Set horizontal flip
-vf, --vflip	: Set vertical flip
-roi, --roi	: Set region of interest (x,y,w,d as normalised coordinates [0.0-1.0])
-ss, --shutter	: Set shutter speed in microseconds
-awbg, --awbgains	: Set AWB gains - AWB mode must be off
-drc, --drc	: Set DRC Level (see Notes)
-st, --stats	: Force recomputation of statistics on stills capture pass
-a, --annotate	: Enable/Set annotate flags or text
-3d, --stereo	: Select stereoscopic mode
-dec, --decimate	: Half width/height of stereo image
-3dswap, --3dswap	: Swap camera order for stereoscopic
-ae, --annotateex	: Set extra annotation parameters (text size, text colour(hex YUV), bg colour(hex YUV), justify, x, y)
-ag, --analoggain	: Set the analog gain (floating point)
-dg, --digitalgain	: Set the digital gain (floating point)
-set, --settings	: Retrieve camera settings and write to stdout
-fw, --focus	: Draw a window with the focus FoM value on the image.


Notes

Exposure mode options :
off,auto,night,nightpreview,backlight,spotlight,sports,snow,beach,verylong,fixedfps,antishake,fireworks

Flicker avoid mode options :
off,auto,50hz,60hz

AWB mode options :
off,auto,sun,cloud,shade,tungsten,fluorescent,incandescent,flash,horizon,greyworld

Image Effect mode options :
none,negative,solarise,sketch,denoise,emboss,oilpaint,hatch,gpen,pastel,watercolour,film,blur,saturation,colourswap,washedout,posterise,colourpoint,colourbalance,cartoon

Metering Mode options :
average,spot,backlit,matrix

Dynamic Range Compression (DRC) options :
off,low,med,high


---
### Some Links

 - [Raspberry Pi einrichten und Kamera verwenden](https://elektro.turanis.de/html/prj164/index.html#VerwendungdesKameraModulsv2)
 - [Raspberry Pi Kamera installieren](https://electreeks.de/raspberry-pi-kamera-installieren-anschliessen/)
 - [Raspberry Pi: Überwachungskamera Livestream einrichten](https://tutorials-raspberrypi.de/raspberry-pi-ueberwachungskamera-livestream-einrichten/)

---
## [The Sunfounder Pan-Tilt Hat](https://docs.sunfounder.com/projects/pantilt-v3/en/latest/)

  - [Repository with the Software](https://github.com/sunfounder/pan-tilt-hat.git)

---
