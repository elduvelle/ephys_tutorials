2022-07-12

Jadhav lab - from John Bladon, many thanks to him & for agreeing to share!  
Slightly modified by El Duvelle  
Questions, comments? Post an [issue](https://github.com/elduvelle/ephys_tutorials/issues) or contact El at https://neuromatch.social/@elduvelle

------------

## Goldplating tutorial for 12 microns Nichrome wire

------------

## Starting notes
- This is for 12 microns diameter Nichrome wire. Larger diameter wire of different material might be easier to plate, although this protocol should still work. Check [this tutorial](https://github.com/elduvelle/ephys_tutorials/blob/main/9_gold_plating_PltIr_17um.md) for larger wire.  
- Before plating: get gold out of fridge (note: it doesn't need to be in the fridge), set up autoplater on a computer, and make sure you have wells, saline solution, and distilled water.
- If you're installing NanoZ for the first time… install from the [WhiteMatter LLC website](https://white-matter.com/products/nanoz/), and drop the ‘electrodes.ini’ file in the appropriate folder, e.g. C:\Users\{your username}\AppData\Local\nanoZ
- VERY IMPORTANT: when dipping tetrodes into solution DO NOT dip them so deep as to dip the cannula in, this will cause gold to flow UP the cannulae, dry, and stick your tetrodes to the cannula.


### Day 1
1. Plug the drive into the adaptor, plug a chosen strip of Millmax of the drive adaptor into the Nanoz adaptor (for 32 tetrode drive, this will need to be repeated 4 times, for each batch of 32 channels), place the corresponding tetrodes in saline solution. Make sure the Nanoz ‘ground’ wire is also connected to the solution.  
2. Test impedance
   1. **Test impedance tab**, cycles 20, pause 2, 1004 Hz
   2. Wires that have an impedance above 10 are likely out, if you can, try to repin
   3. feel free to save the result file as a text file by clicking on the save icon
3. ‘Bubble-testing’ (= cleaning tetrode tips):
   1. **DC Electroplate tab**, fixed plating time,  interval 2s, plating current +1µA (can probably be higher)
   2. Impedance should drop below 2 mOhms
4. Dip the tetrode tips in **distilled water** a few times to clean the saline, let it dry a bit
5. Gold-plating
   1. Dip the tetrodes in the gold solution, connect the corresponding Nanoz ‘ground’
   2. Plate at -0.5 µA for 1 sec, match 500 kOhms, 5 passes. Impedance should drop to around 450 kOhms
   3. This is the step where you can deselect wires that haven’t dropped below 1 MOhm (in the ‘probe’ schematic), and you will want to replace these tetrodes
6. Plate at -0.05 to -0.025µA for 1 sec, 10 passes, match 250 kOhms
   1. Wires should end around 250 kOhms
7. Repeat for each connector
8. at the end: empty all wells contents (back into their original syringe), make sure to keep the gold solution protected from light (and manipulate it with gloves on). If the saline or distilled water seem dirty, discard them instead.

## Day 2
- Similar installation as day 1
- optional: measure impedances again in saline
- If you replaced any tetrode, start with step 1 on day 1
- For the tetrodes that were already plated:
   1. Plate at -0.05 to -0.025µA for 1 sec, 10 passes, match 250 kOhms
   2. Wires should end around 250 kOhms
   3. Do this two to three times, the second time match to 240 kOhms, and the third time match to 230 kOhms  
Note: Brad Pfeiffer says that he sometimes does this for about a week until the impedances remain at low values!

## Troubleshooting:
- wires that are around 500 kOhms may have “bubbles” on them and you can try to lift the drive out of the solution and place them back.  You can also try to “burn off” / clean that wire at +1 µA again, but it will return to low (or is it high?) impedance rapidly so be patient the second time around.
- If the wire is above 10 mOhms, it is out, check at the EIB pin.
- If many wires are not going down in impedance, switch out your gold to new fresh gold (or try to mix the solution first)
- DO NOT DESCEND DRIVE SO FAR THAT THE MOUTH OF THE GUIDE CANNULA IS DIPPED INTO THE GOLD SOLUTION
- If any wires are now above 1MOhms, they will need to be recut or replaced;  any wires which are now below 100kOhms could be ‘reverse-plated’ or cut.  
