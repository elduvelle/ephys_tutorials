## Ephys untethered recording with Trodes (SpikeGadgets)
### Last updated with Trodes 2.4.0

### Hardware needed:

- MCU (to record the environmental data during recording) + its antenna to send the sync signal to the headstage
- (optional) Logger Dock (for extracting data from the SD card after recording)
- Headstage set for wireless recordings
- Charged battery
- Enabled SD card

### Recording procedure

#### 1. To do beforehand, only once  
  1.1. (check MCU firmware)  
  1.2. Create a workspace for merging, and one for logging (no channels)  
    1.2.1. Merging workspace should be like the screening workspace: with all the recording channels active. This can be updated after each screening session.  
- Create or open the workspace that you normally use for tethered recordings (with the right channels, tetrode mapping etc)
- Connect the MCU that will be used during recording, via USB, and the headstage that will be used (WITHOUT the SD card)
- (optional) connect to the video and prepare the tracking settings, save the geometry
- Update the settings of both to have 'Session ID' on, the same RF channel, and the same sampling rate.
![image](https://github.com/vandermeerlab/mvdmlab-protocols/assets/64431932/73225c73-5c20-4235-a487-43a0db1d11f8)
  
- Ensure that the Headstage has the desired options set on (e.g. accelerometer)
- Save the workspace ('merging workspace')  
    -> this merging workspace will be used after the untethered recording has been done to merge it with the ephys channels.

    1.2.2. Logging workspace should have zero channels, but links to the video, MCU, and other data streams that we want to connect during the recording e.g. ECU, accelerometer, etc. Make it and save it.
- create or open the workspace
- **set channel count to 0**
- add relevant data streams (e.g. for ECU select it from the Hardware Devices menu > +Add Device)  
- Make sure that 'ZMQ socket' is enabled!!  
- save the workspace ('data logging workspace')
- reopen it in Trodes and set the MCU to the desired options (connect via USB for this): Session ID mode on, correct RF channel

#### 2. To do every time before a recording  
  2.1. ensure that battery is charged (use Logger Dock to charge it)  
  2.2. connect MCU to computer (usb or ethernet), connect the RF transceiver (Aux 1 port), switch it on   
  2.3. enable SD card for recording: either insert in MCU and press the 0_0 button until it goes back to green, or use the LoggerDock 'enable for recording' option  
  2.4. Start Trodes, with the 'data logging workspace', connect it to MCU  
  2.5. (optional) Ensure that ECU is connected to MCU via HDMI, start it  
  2.6. Connect the battery (and optionally LEDs) to the untethered headstage, insert the enabled SD card.  
![image](https://github.com/vandermeerlab/mvdmlab-protocols/assets/64431932/bcc2813c-4a87-436d-8922-67ef03f5f07a)

#### 3. When ready for recording  
  3.1. If using tracking: click on Video, load or create the appropriate geometry, start tracking  
  3.2. Connect the headstage to the rat, make sure the SD card is in, switch the headstage on: the tracking LED (if connected) should switch on, the headstage LED indicators should both blink twice (orange & red) indicating power to the headstage, then the orange one should slow blink ('breathing') indicating that the SD card is enabled. Mine alternates this and 4 fast orange blinks which are supposed to indicate start of recording...  
  3.3. Select Stream from source: the headstage will start recording: it will do 4 orange blinks and then stop the 'breathing' pattern.  
  3.4. Select 'New recording...' then choose a filename: the MCU will start recording. The Headstage should now xxx    
  -> check why the 'RF sync' channel doesn't show anything
  -> check why the hs doesn't make any light

#### 4. To end recording  
  4.1. Hit the pause button (stops the MCU from recording), close file, disconnect the stream (stops the headstage from recording: it should do a slow red breathing indicator)  
  4.2. Switch the headstage off  
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
    5.3.2. Select the environmental recording file (might be already populated if opened from Trodes)  
    5.3.3. Select the right neural recording file (from the SD card)  
    5.3.4. Ensure that the merged filename is correct and click START  (Note: if a problem occurs, try replacing the SD card in the reader)
The new 'merged' file is the one that needs to be used in future processing steps, but note that some of the files (e.g. position data) will not have the 'merged' suffix.  
For error messages at this stage, see [DataLoggerGui doc](https://docs.spikegadgets.com/en/latest/basic/DataLoggerGUI.html)  

#### 6. Final operations
  6.1. Potentially charge the battery using the logger dock, for next time  
  6.2. Potentially re-enable the SD card

### Additional notes

- the logger dock can be used instead of the MCU to record, but I haven't made it work yet.
- it seems easier to have 1 headstage specifically configured for tethered recordings and a different one for untethered recordings
- settings of headstage or MCU can only be changed if connecting to the MCU via USB

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
