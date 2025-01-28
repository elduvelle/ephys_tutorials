2015-08-28

Originally from the Caccucci lab, many thanks to them!

Questions, comments? Post an [issue](https://github.com/elduvelle/ephys_tutorials/issues) or contact El at https://neuromatch.social/@elduvelle_neuro

------------

## Goldplating tutorial for 17.5 microns Platinum-Iridium wire

------------

## Starting notes
- This has been tested for 17.5 microns Platinum-Iridium wire with good results. Do let me know if it works well for you (or not) with other types of wire.
- Check [this other tutorial](https://github.com/elduvelle/ephys_tutorials/blob/main/1_gold_plating_Nichrome_12um.md) for smaller wire.

- Before plating: 
  - prepare plating wells: distilled water & saline solution; gold can be retreived when needed.
  - If you're installing NanoZ for the first time… install from the [WhiteMatter LLC website](https://white-matter.com/products/nanoz/), and drop the ‘electrodes.ini’ file in the appropriate folder, e.g. C:\Users\{your username}\AppData\Local\nanoZ
  - in the Nanoz software, load the adaptor and eletrode file corresponding to your drive. Check the nanoz documentation to make a different electrode file.
  - make the final cut for your tetrodes before plating (but you can also use the nanoz to test impedances pre-cut, at any times).

## Plating tips:
- always clean tetrodes in dH2O (dip them a few times), then let them dry (at least a few seconds) before dipping them in the gold solution. This is to avoid contamination of the solution.
- in general, avoid contaminating the gold solution with anything. Only use a small amount from the original batch if possible, reuse it until it stops working (impedances do not lower, or worse, increase) or looks different (e.g. cloudy). Keep the original batch in a sealed container possibly away from light.
- do not lower tetrodes in the saline or gold until the cannula touches the liquid: this could cause gold or saline to flow up then dry and potentially stick the tetrodes. Clean with distilled water if this happens.
- if impedances lower too much on a tetrode (possible short), reverse the plating by reversing the polarity of the stimulation.
- Gold-plating can be done on the morning of implantation surgery, or the day before, ideally always test and re-plate if necessary just before surgery.

## Plating protocol

### Step 1: original testing

|  |   |
| --- | --- |
| Solution | SALINE |
| Tab | *test impedance*|
|Test frequency | 1004 Hz|
|Cycles | 20 |
|Pause | 2 s|

Impedances should be around between 1-3 M Ohms  

### Step 2: cleaning ('bubble-test')

|  |   |
| --- | --- |
| Solution | SALINE|
| Tab | *DC electroplate*|
| Mode | Fixed plating time|
| Plating Current | Max: + 11.890 uA|
|Interval | 1 s |
|Pause | 1 s|

Individual test of impedance
Start “autoplate”

This procedure should reduce the impedance of all connected channels.

## Step 3: pre-plating test

Same as Step 1  
Impedances should now be around 300-500 kOhms. If they are too high, you can re-try the cleaning step, or cut the tetrodes again to get a nicer cut.

## Step 4: plating

> [!WARNING]
> Make sure to dip tetrodes in distilled water, then leave them to dry a bit, before dipping them in the gold solution.

|  |   |
| --- | --- |
| Solution | GOLD|
| Tab | *DC electroplate*|
| Mode | Matched impedance|
| Plating Current | -0.250 uA|
|Target | 200 kOhms|
| Test frequency | 1024 Hz |
|Runs | 10|
|Interval| 1s|
|Pause |2s|

Repeat step 4 if necessary (i.e. all tetrodes have not reached the target impedance).
