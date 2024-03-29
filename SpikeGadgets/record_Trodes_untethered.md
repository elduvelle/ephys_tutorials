## Ephys untethered recording with Trodes (SpikeGadgets)
### tested with:
- Trodes 2.3.4 <-- USE THIS VERSION
- Trodes 2.4.0
- Trodes 2.4.2

FAILS with:
- Trodes 2.5.0
- and possibly 2.4.2

### Hardware needed:

- MCU (to record the environmental data during recording) + its antenna to send the sync signal to the headstage
- Logger Dock (for extracting data from the SD card after recording)
- Headstage set for wireless recordings
- Charged battery
- Enabled SD card

### Recording procedure

#### 1. To do beforehand, only once  
  1.1. Check MCU firmware (mine used to be 3.18.0 which was working fine with 2.3.4, and now has been upgraded to 3.20.2, which will not work with some older versions, for example Trodes 2.2.3). To do this, start a recent Trodes version and click on Hardware report or start an earlier version and click on it in the modify workspace menu  
  1.2. Create a workspace for **merging**, and one for **logging** (no channels)  
    1.2.1. Merging workspace should be like the screening workspace: with all the recording channels active. This can be updated after each screening session.  
- Create or open the workspace that you normally use for tethered recordings (with the right channels, tetrode mapping etc)
- Connect the MCU that will be used during recording, via USB, and the headstage that will be used (WITHOUT the SD card)
- (optional) connect to the video and prepare the tracking settings, save the geometry
- Update the settings of both to have **'Session ID' on**, the same RF channel, and the same sampling rate.
![image](https://github.com/vandermeerlab/mvdmlab-protocols/assets/64431932/73225c73-5c20-4235-a487-43a0db1d11f8)
  
- Ensure that the Headstage has the desired options set on (e.g. accelerometer)
- Save the workspace (`merging workspace`)  
    -> this merging workspace will be used after the untethered recording has been done to merge it with the ephys channels.

    1.2.2. Logging workspace should have zero channels, but links to the video, MCU, and other data streams that we want to connect during the recording e.g. ECU, accelerometer, etc. Make it and save it as `logging workspace`.
- create or open the workspace
- **set channel count to 0**
- add relevant data streams (e.g. for ECU select it from the Hardware Devices menu > +Add Device)  
- **Make sure that 'ZMQ socket' is enabled!!**  
- save the workspace (`logging workspace`)
- reopen it in Trodes and set the MCU to the desired options (connect via USB for this): Session ID mode on, correct RF channel, then save again

    1.3. IMPORTANT Ensure that the Logger Dock will not interfere with the recordings  
- if the logger dock and the headstage are on the same RF channel (say, the default, 2) and the logger dock is on during the recording, it will keep sending a 'stop recording' message to the headstage and no recording will happen.
- to avoid this, setup the logger dock RF channel to be something else than the Headstage and MCU (say, 4). You will then be able to use the logger dock while recording (for example to extract data from the previous recording session) without interference.

#### 2. To do each time before a recording  
  2.1. ensure that battery is charged (use Logger Dock to charge it until the LED is green)  
  2.2. connect MCU to computer (usb or ethernet), connect the RF transceiver (Aux 1 port), switch the MCU on   
  2.3. enable SD card for recording: either insert in MCU (if firmware >v18) and press the 0_0 button until it goes back to green, or use the LoggerDock 'enable for recording' option with the sd card inside the logger dock  
  2.4. switch your tracking camera on  
  2.5. Start Trodes with the `logging workspace`, connect it to MCU  
  2.6. (optional) Ensure that ECU is connected to MCU via HDMI, start it & connect to it in Trodes  
  2.7. Connect the battery (and optionally LEDs) to the untethered headstage, insert the enabled SD card.  
![image](https://github.com/vandermeerlab/mvdmlab-protocols/assets/64431932/bcc2813c-4a87-436d-8922-67ef03f5f07a)

#### 3. When ready for recording  

TLDR: enabled card in HS -> switch HS on -> start streaming in Trodes -> start recording in Trodes IN THAT ORDER

In more details:  
  3.1. If using tracking: click on Video, load or create the appropriate geometry, start tracking  
  3.2. Connect the headstage to the rat, make sure the SD card is in, switch the headstage on: the tracking LED (if connected) should switch on, the headstage LED indicators should both blink twice (orange & red) indicating power to the headstage, then the orange one should slow blink ('breathing') indicating that the SD card is enabled. Mine alternates this and 4 fast orange blinks which are supposed to indicate start of recording...  
  3.3. Select Stream from source: the headstage will start recording: it will do 4 orange blinks and then stop the 'breathing' pattern.  
  3.4. Select 'New recording...' then choose a filename, let's say `Recording_file`; the MCU will start recording. The Headstage should now xxx  (blink? do nothing? unclear)  
  -> check why the 'RF sync' channel doesn't show anything  
  -> check why the hs doesn't make any light -> I think this might be changed in future versions

#### 4. To end recording  
  4.1. Hit the pause button (stops the MCU from recording), close file, disconnect the stream (stops the headstage from recording: it should show a slow red breathing indicator)  
  4.2. Switch the headstage off and retrieve the SD card  
you now have two recording files: the 'neural recording' on the SD card and the 'environmental recording' on the computer.  

#### 5. Post-recording merging  
  5.1. **using the Logger Dock**  
    5.1.1. Connect the logger dock to the computer and insert the SD card in it  
    5.1.2. Start the Data Logger GUI  
   
  5.2. **using the MCU** (To Be Tested; needs to be running firmware version 3.19)  
    5.2.1. Connect the MCU via USB to the computer and insert the SD card in it (via the adapter).  
    5.2.2. Open Trodes, go to playback mode, open the file recorded locally, File>Merge with logger data  

  5.3. Common to both  
    5.3.1. Ensure that 'Merge logger data with environmental data' check box is ticked  
    5.3.2. Select the environmental recording file (might be already populated if opened from Trodes) - in our case, 'Recording_file'  
    5.3.3. Select the right neural recording file (from the SD card) - 'merging_workspace'  
    5.3.4. Ensure that the merged filename is correct and click START  (Note: if a problem occurs, try replacing the SD card in the reader)  
The new 'merged' file is the one that needs to be used in future processing steps, but note that some of the files (e.g. position data) will not have the 'merged' suffix.  
For error messages at this stage, see [DataLoggerGui doc](https://docs.spikegadgets.com/en/latest/basic/DataLoggerGUI.html)  

#### 6. Final operations
  6.1. Potentially charge the battery using the logger dock, for next time  
  6.2. Potentially re-enable the SD card  
  6.3. To check the merged recording:  
      6.3.1. Open Trodes  
      6.3.2. Playback File: find and open your merged file  
      6.3.3. (optional) Video > find and open your video file  
      6.3.4. Press Play to see your recording!  

### Additional notes & known bugs

- the logger dock can be used instead of the MCU to record, but I haven't made it work yet.
- it seems easier to have 1 headstage specifically configured for tethered recordings and a different one for untethered recordings
- settings of headstage or MCU can only be changed if connecting to the MCU via USB
  
- **versions 2.4.2 and 2.5.0** (at least) have a bug where they 'sometimes' change the settings of the MCU. This will make future connections to the MCU impossible and / or trigger an error at the time of streaming. It will also prevent proper extraction of the data from the SD card. IF this happens, you need to 1) make sure your MCU firmware is up to date (v. 3.20.2), 2) reinitialize the settings of the MCU with the 'reset_MCU_settings' code provided by SpikeGadgets and 3) once reset and restarted, set the MCU settings to the desired ones (see paragraph 1.2)

---

### Useful links

[Trodes Untethered recordings documentation](https://docs.spikegadgets.com/en/latest/basic/Untethered.html)  
[Headstage manual](https://spikegadgets.wpenginepowered.com/wp-content/uploads/2022/11/HH128_Headstage_Manual_Rev2c_1122.pdf)  
[Data logger GUI info](https://docs.spikegadgets.com/en/latest/basic/DataLoggerGUI.html)  
[How to merge using the command line](https://docs.spikegadgets.com/en/latest/basic/SDFunctions.html)  
[RF Transceiver](https://spikegadgets.com/products/rf-transceiver/)  

#### Headstage Status Indicators
![image](https://github.com/vandermeerlab/mvdmlab-protocols/assets/64431932/8731342c-50c1-4565-8930-9090bd8a98d4)  
Note: When the MCU and headstage are configured for untethered recording and the RF transceiver is connected to the MCU, the headstage’s yellow LED will blip intermittently. 
