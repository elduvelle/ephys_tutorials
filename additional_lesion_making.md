### 1. (Probably) the best lesion parameters, from Anna Gillespie (thank you for sharing!)

- Lesions are performed 24h before perfusion (under isoflurane anaesthesia)
- Lesion parameters: 30 μA of positive current for 3s, on 2-4 channels per tetrode
- after 24h, proceed with perfusion (PBS followed by 4% paraformaldehyde in 0.1M PB)
- leave the entire skull in PFA for 24h with the tetrodes still inside the brain
- after additional 24h, pull tetrodes up and remove brain

This is how it _should_ look like:
![image](https://github.com/elduvelle/ephys_tutorials/assets/64431932/5ad0c8d6-aa8b-4e03-85a3-888354c439b5)

Source:
[Gillespie et al., 2021](https://www.sciencedirect.com/science/article/pii/S0896627321005730?via%3Dihub)  
lesions method actually described in: [Sosa et al., 2020](https://www.sciencedirect.com/science/article/pii/S0896627319310086)

This is how it looks like when I do it on 13 um Nichrome wire (20 uA instead of 30 uA, tried 2s of stimulation for some tetrodes, but couldn't see those lesions at all, so definitely use 3s):
![IMG_9980](https://github.com/elduvelle/ephys_tutorials/assets/64431932/9bb1da25-2d38-4564-bc50-1f83e5c837fd)
![IMG_9981](https://github.com/elduvelle/ephys_tutorials/assets/64431932/eb7e6057-3491-4556-a5d9-dbd6b39ebfab)


### 2. alternative device to make lesions

![lesion-maker](https://github.com/elduvelle/ephys_tutorials/assets/64431932/035f828b-4bcb-44f7-84ca-6cef336667d8)

method:

|parameter |value   |
|----------|--------|
|power:    |on      |
|audio:    |on      |
|mode:     |unipolar|
|range:    |100uA|
|% range:  |e.g. 30 (for 30 uA)|
|Polarity select:| red light on right/red for positive current|
|Output:   |on|

Red output = contacting channel to lesion  
Black output = connected to drive ground, grounded part of cone, or, alternatively, rat skin via a saline-imbibed tissue

Hold DC/test up (ON) to make the lesion, once the circuit is ready. Release before moving on to the next channel.  
*TIP: Low-pitch sound indicates good connection, high-pitch sound indicates a disconnected circuit.*



