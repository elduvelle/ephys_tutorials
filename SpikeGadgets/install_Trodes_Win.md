## This describes the procedure to install SpikeGadgets software on WINDOWS specific to our lab

### Useful links:
[general SpikeGadgets documentation](https://spikegadgets.com/documentation/)  
[Trodes install documentation](https://docs.spikegadgets.com/en/latest/basic/Install.html#)  
[Trodes software](https://bitbucket.org/mkarlsso/trodes/downloads/)  
[Headstage doc](https://spikegadgets.wpenginepowered.com/wp-content/uploads/2022/11/HH128_Headstage_Manual_Rev2c_1122.pdf)  
[MCU, logger dock doc](https://spikegadgets.wpenginepowered.com/wp-content/uploads/2023/02/Control_Units_Rev2a_0223.pdf)  


### Detailed procedure (most of which from the Trodes install link above)

1. Install the [FTDI D2XX Driver](https://ftdichip.com/drivers/d2xx-drivers/). Best to use the “setup executable” listed in the comments for Windows.
2. Download the latest release of the Trodes software suite [here](https://bitbucket.org/mkarlsso/trodes/downloads/)
3. Uncompress the downloaded folder and copy to a desired location on your machine.
4. Run the included program vc_redist.x64.exe to install the required Microsoft plug-ins.
5. Create a folder to save the collected data on the computer (ideally **NOT** in the same drive as Trodes)
6. Choose an Ethernet plug to connect the MCU. This should not be shared with anything else.   
  6.1. Configure the network adaptor that the MCU will connect to: set to IPV4, Adress 192.168.0.2, Subnet 255.255.255.0. Note, on Win10, it asks about Subnet length instead, which should be 24, but may not work, in which case try to change those settings in the "change adaptor options" settings for ipv4, directly   
  
  6.2. (not fully sure about this) Set up the MTU of the connection. Network connection > right click on the connection to setup > Properties> configure> advanced > Jumbo Packet> set to 9014 bytes. To check that it did the change, open a command line console and type netsh int ipv4 show subinterface. it should have changed the MTU setting.  
  6.3. Add these keys in the registry (DefaultReceiveWindow & DefaultSendWindow):  
  ![image](https://user-images.githubusercontent.com/64431932/235474973-4df5b6bc-95bd-40f0-bdc5-a60ea7363e77.png)  
  6.4 If using the Network card recommended by SpikeGadgets: [Intel Gigabit CT PCI-E Network Adapter](https://www.amazon.com/Intel-Gigabit-Network-Adapter-EXPI9301CTBLK/dp/B001CY0P7G): go to the advanced settings for the card itself and set the "hardware receive buffer" to the maximum allowed value (in my case: 2048)  
![image](https://github.com/vandermeerlab/mvdmlab-protocols/assets/64431932/09f9ac0a-5616-4c2a-9425-5301391ede6d)

7. If using Ethernet Cameras e.g. Vimba: (OPTIONAL: seems to work without it) 
  7.1. Make sure to plug it in a separate Ethernet card from Trodes, otherwise it can interfere / not be detected  
  7.2.  Install [Vimba Viewer](https://www.alliedvision.com/en/products/vimba-sdk/) to test the camera and install the drivers (*note: it might work without this step*)  
  7.3. In Vimba Viewer install choose the 'demonstration software' and choose to install drivers at the end  
  7.4. Check that you can see the camera feed in the software (click on the camera and click on play)  
  
 8. If using maze automation  
  8.1 Install [Matlab](https://login.mathworks.com/embedded-login/landing.html?cid=getmatlab&s_tid=gn_getml) - the latest version *should* work  
  8.2 (probably optional) Choose these toolboxes: Audio; Computer Vision; Curve Fitting DSP System; Data Acquisition; Deep Learning; Image Acquisition; Image Processing ; Optimization; Parallel Computing; Reinforcement Learning; Signal Processing; Statistics and Machine Learning; Wavelet  
  8.3 (optional) Install [Github Desktop](https://desktop.github.com/) for easy interfacing with Github   
  8.4. clone the appropriate automation repo (e.g. [nap_automation_pilot4](https://github.com/c-holland/nap_automation_pilot4))  
  8.5. Open Statescript from within the extracted Trodes folder and set the path to Matlab and the path to the automation statescripts & Matlab script folder  
  8.6. Recreate the Macros in statscript that we use (see addendum at the end)
  8.7. Update the Matlab code paths with correct paths for the current computer (favourite, for testing + `nap_get_paths`)  
  8.8. Test it!  
    8.8.1. If getting errors: make sure that all the Trodes/Resources/matlab server functions are present in the Matlab folder that your scripts are in; alternatively, copy your matlab scripts to that folder and set it as the appropriate code folder in Statescript  
  
 9. If using Filezilla to backup data  
  9.1. Downlowad [Filezilla](https://filezilla-project.org/) -> 'download filezilla client'  
  9.2. Connect to the lab's server (see instructions on slack #server channel) & create a bookmark to connect your local data folder to one on the server



  

10. Double-click on Trodes.exe to run.  
  10.1. (optional) Download any .rec file from the server to see if it works ('Playback' option in Trodes)  
  10.2. Ideally, reuse a previously-created config file (workspace), see for example in the server, Eleonore/Screening Documents   
  10.3. See other protocols (Trodes tethered recording / Trodes untethered recordings) to do a recording! [TODO]



----
#### Addendum: macros for Statescript in RR1

![image](https://github.com/vandermeerlab/mvdmlab-protocols/assets/64431932/f2b68c87-44f6-4ea1-ae9c-6cbd55bb9020)



