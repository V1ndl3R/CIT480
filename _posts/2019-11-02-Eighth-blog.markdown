This week I made a PWNAGOTCHI, it is a an A2C-based "AI" that utilizes bettercap. That will automatically find and 
capture handshakes for wifi networks that it is exposed to.  The hardware needed is a Raspberry pi zero and a 
waveshare eink 2.13" display.  It is very simple to make and install the code.  I had to solder the
leads onto the Pi but that was very easy.  You can find a ton of tutorials online that will show you how to solder.
The model of the waveshare that I got was a hat version so it just connects once you completed the soldering.

There are two methods of installing pwnagotchi, the easiest method is just to flash an image of the latest pwnagotchi
release that you can get from pwnagotchi.ai.  I used balena Etcher to install it onto a micro SD card.  There are 
some setup files that you can make or edit before you boot.

It is recommended that you create a config.yml file and place it in your boot partition. It should look like this:
main:

  name: 'pwnagotchi' <--- You can rename it here.

  whitelist:

    - 'YourHomeNetworkMaybe'  <-- Place the SSID of any networks that you do not want to hack here.

  plugins:

    grid:

      enabled: true

      report: true

      exclude:

        - 'YourHomeNetworkMaybe'   <-- same here you can place multiple if you need to
 
        - 'addmore if you want'


ui:

    display:

      type: 'waveshare_2'

      color: 'black'



The rest you can leave the same, change the display if you used a different one or version.  After that you can just
plug it in and it will do it thing.  It will detect and capture any network not listed on the whitelist.
There are 3 different modes, and depending on what usb port you connect to will determine what mode it boots into.
I would recommend connecting the power to the first port so that it will boot into AUTO and then AI mode.  After you 
have grabbed a few handshakes and witnessed how it works you can connect it to the data port and connect the USB to
your computer.

This will boot it into Manu mode and will allow you to connect to the Raspberry pi zero.
You can connect to the the bettercap UI when it is in the mode via http://pwnagotchi.local (change the name if you did)
Once your device has booted up, it will appear as a network device.  You can now assign it a IP address, 10.0.0.1 
for example, the netmask should be 255.255.255.0.  After you completed this you can connect via ssh pi@10.0.0.2.  If
this does not work you can try to ping it to see if it is configured correctly.  I did not have any issues connecting
to my pi.  When you connect the default password is raspberry it is recommended that you change it with passwd 
command.  There are a ton of features that you can play with and tweak to your liking.  I have not had much time to 
play with the files yet.
