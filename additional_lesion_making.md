### 1. (Probably) the best lesion parameters, from Anna Gillespie (thank you for sharing!)
_note: I haven't personally tested these yet_

- Lesions are performed 24h before perfusion (under isoflurane anaesthesia)
- Lesion parameters: 30 μA of positive current for 3 s, on 2-4 channels per tetrode
- after 24h, proceed with perfusion (PBS followed by 4% paraformaldehyde in 0.1M PB)
- leave the entire skull in PFA for 24h with the tetrodes still inside the brain
- after additional 24h, pull tetrodes up and remove brain

This is how it _should_ look like:
![image](https://github.com/elduvelle/ephys_tutorials/assets/64431932/5ad0c8d6-aa8b-4e03-85a3-888354c439b5)

Source:
[Gillespie et al., 2021](https://www.sciencedirect.com/science/article/pii/S0896627321005730?via%3Dihub)  
lesions method actually described in: [Sosa et al., 2020](https://www.sciencedirect.com/science/article/pii/S0896627319310086)


### 2. alternative device to make lesions
![IMG_8043](https://github.com/elduvelle/ephys_tutorials/assets/64431932/ee670de0-ceee-4267-9ca9-799696cbb506)
method:

|parameter |value   |
|----------|--------|
|power:    |on      |
|audio:    |on      |
|mode:     |unipolar|
|DC/test:  |on      |
|range:    |100uA|
|% range:  |e.g. 30 (for 30 uA)|
|Polarity select:| red light on black/ground for negative current|
|Output:   |on|

Red output = contacting channel to lesion
Black output = connected to drive ground (or, alternatively, rat skin with a wet tissue)



