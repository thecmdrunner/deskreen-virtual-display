This guide uses [Deskreen](https://github.com/pavlobu/deskreen) on Pop! OS 20.04

# 1. Virtual Display Output

Deskreen can share any display as long as it is detected via `xrandr`, but to be able to have a display show up exlusively on a secondary device, there needs to be an unused display output. Most GPUs and laptops have additional display-out ports that can be used. But in my case, I use my TV as a primary display, while casting my laptop's screen to my phone, as my laptop's display doesn't work anymore.

## Add a Virtual Output

The idea is to make the system think that a display is connected to an unused display-out port (HDMI / DVI / DisplayPort) and sharing its contents to our secondary device via Deskreen.

### A. Open up terminal app and enter `xrandr --listmonitors` to check out all available display ports.

The output will be something like this.

```bash
Monitors: 2
 0: +*HDMI-A-0 1920/575x1080/323+0+0  HDMI-A-0
 1: +eDP 1366/344x768/193+1920+0  eDP
```

As you can see, I have total 2 display outputs, `HDMI-A-0` (HDMI Port, which is plugged in) and `eDP` (laptop's primary display, which is currently unused).

`*` means that the display is currently active.

### B. Make existing output virtual:

#### i. Declare Variables:

Open `make-virtual-output.sh` and edit the variables accordingly.

In my case, the values will be:

```bash
# REPLACE THE VALUES WITH YOUR OWN:
v_name=eDP                # Unused output that you want to use for Deskreen
v_width=1366              # Put the max for your display (eg. 1920)
v_height=768              # Put the max for your display (eg. 1080)
v_position=right-of       # Options: right-of | left-of | above | below 
current_output=HDMI-A-0   # Referemce display to use for positioning

# My command will look like: xrandr --output eDP --mode 1366x768 --right-of HDMI-A-0
```

#### ii. Enable display via `xrandr`

Now run the following commands to enable the virtual display.

```bash
chmod +x ./make-virtual-output.sh
./make-virtual-output.sh
```

<p>
<details>
<summary>Here is my output after enabling virtual output for `eDP`</summary>
<br>
 
`*` means that the display is currently active.
 
 ```bash
EXECUTING: xrandr --output eDP --mode 1366x768 --right-of HDMI-A-0 

Screen 0: minimum 320 x 200, current 3286 x 1080, maximum 16384 x 16384
eDP connected 1366x768+1920+0 (normal left inverted right x axis y axis) 344mm x 193mm
   1366x768      60.00*+  47.99  
   1280x720      60.00  
   1024x768      60.00  
   800x600       60.00  
   640x480       60.00  
   1920x1080     60.00  
HDMI-A-0 connected primary 1920x1080+0+0 (normal left inverted right x axis y axis) 575mm x 323mm
   1920x1080     60.00*+  60.00    50.00    59.94    24.00    23.98  
   1680x1050     59.88  
   1280x1024     60.02  
   1440x900      60.00  
   1280x960      60.00  
   1360x768      60.02  
   1280x800      59.91  
   1280x720      60.00    50.00    59.94  
   1024x768      60.00  
   800x600       60.32    56.25  
   720x576       50.00  
   720x480       60.00    59.94  
   640x480       60.00    59.94  
   720x400       70.08 
```

</br>
</details>
</p>

### C. Verify if the new output is detected in Display Settings

![Screenshot of Display Settings](https://imgur.com/Ze2tbFP.png)


# 2. Easy Part!

Now that all the technical jargon is over, we can finally head to the easy part!

### A. Get your Deskreen working

Go ahead and download [Deskreen](https://deskreen.com) client as a `deb` or `AppImage` file (depending on your system), from their official website.

### B. Connect your secondary device

![Screenshot of Deskreen](https://i.imgur.com/QiG4Bdc.png)

I am using my Android Phone as a secondary device here, but feel free to use any reasonable device with a recent enough browser (Firefox, Chrome, Safari)

After opening Deskreen,

<ul><li>If you are using a mobile phone, scan the QR code shown there, which will open a link in the browser</li><li>Or, you can simply enter the URL shown below the QR Code in the browser of another device.</li>

But remember, the link changes when the remote device is disconnected, and you will have to allow the device everytime.

![Screenshot of Deskreen Authentication](https://i.imgur.com/wDTqMnL.png)

<li>Deskreen will then ask you if you want to allow the device while trying to connect.</li>
 

![Screenshot of Deskreen Sharing Choice](https://i.imgur.com/6cHOP80.png)

<li>From there, choose between sharing an entire screen, or just a specific window.</li>
 

![Screenshot of Deskreen Screens](https://i.imgur.com/OEjpmef.png)

<li>I am going to share the virtual screen that I just created above!</li>
 

![Screenshot of Deskreen Confirm](https://i.imgur.com/daSl74v.png)

<li>Confirm the choices, or change something if you need to.</li>
 

![Screenshot of Phone Browser](https://i.imgur.com/qtLpHiC.png)

<li>And, Voila! I have my phone as a secondary display for my laptop, which works wirelessly! :D</li>

You can set the quality to `auto` or anywhere from `25-100%`, as well as flip the screen from the ⚙️ icon.

But hey, don't close the main Deskreen app, keep it minimized, as it doesn't run in the background and will terminate your running remote displays :)
 
</ul>

Thank you for reading this far 😉, and feel free to leave a comment for suggestions, queries or issues you are facing! 
