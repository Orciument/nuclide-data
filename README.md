# Nuclide Data

This repository includes a JSON Array containing 3367 Nuclide, that should be pretty much all that are currently known in February 2023.
The data is from [iaea.org](https://iaea.org), more on that under [Sources](https://github.com/Orciument/nuclide-data/edit/main/README.md#sources)

I created this repository because I got frustrated when i needed this data for a personal Rust, because i could not find this data in a Machine Readable.
So i decided to compile the data myself and publish it again to help people who need this data in the future. 

## Disclaimer 

This Data should not to be used for any scientific work.
I do not claim that this data is neither reliable, complete, or correct!
So use it at your own risk!

## Licence/Copyright

As far as i am concerned you can to anything with the data that you want, 
**but** this is not my data, so you should check the [iaea](https://nucleus.iaea.org/Pages/Others/Terms-Of-Use.aspx) Page on Copyright.

## Format/Syntax
The JSON Element consists of the following fields (in this Order):
| Name | Type   | Value                            |
|------|--------|----------------------------------|
| z    | Number | Number of Protons                |
| n    | Number | Number of Neutrons               |
| name | String | The abbreviated Name of the Atom |
| life | Number | The Half-life of the Nuclide in seconds | 
| mode | String | a Char code that indicates the type of decay |

### Radiation Modes
Explanation: 
- https://de.wikipedia.org/wiki/Liste_der_Isotope#Legende_der_Zerfallsarten 
  (This is in German, because the English Wikipedia page does not have this Table that shows the difference in protons and neutrons after the decay process)
- https://www-nds.iaea.org/relnsd/vcharthtml/guide.html#gs_de

| Symbol | Decay-Type (my understanding) |
|--------|------------|
| B- | BetaMinus |        
| N | N |                
| 2N | 2× N |               
| P | P |                
| A | Alpha |             
| EC | BetaPlus |         
| EC+B+ | BetaPlus |      
| 2P | 2× P |               
| B+P | BetaPlus followed by P |      
| B-N | BetaMinus followed by N |     
| B-2N | 2× BetaMinus followed by N | 
| B+ | BetaPlus |        
| 2B- | 2× BetaMinus |    
| 2EC | 2× BetaPlus |       
| 2B+ | 2× BetaPlus |     
| SF | Spontaneous fission |               
| S | Stable |                

There are some Symbols that i have listed below a resulting in the same decay types, that is a simplification that i made because i could not find where the difference lies, and i quiet frankly did not need further detail for my project, 
but these different symbols are included in the data so you can make the distinction if you want.

### Examples

```
{ \"z\":0, \"n\":1, \"name\":\"Nn\", \"life\":\"613.9\" , \"mode\":\"B-\" },

{ \"z\":0, \"n\":4, \"name\":\"N\", \"life\":\"1.7547604425822527e-22\" , \"mode\":\" \" },

{ \"z\":0, \"n\":6, \"name\":\"N\", \"life\":\" \" , \"mode\":\" \" },

{ \"z\":1, \"n\":0, \"name\":\"H\", \"life\":\" \" , \"mode\":\"S\" },
```

## Sources

- https://www-nds.iaea.org/relnsd/vcharthtml/VChartHTML.html
- https://www-nds.iaea.org/relnsd/vcharthtml/api_v0_guide.html (API)
- https://nds.iaea.org/relnsd/v1/data?fields=ground_states&nuclides=all (API Call)

### Methodology

I have downloaded the CSV File with the given API Call, i then translated these Collums into the JSON Objekts:
- z
- n
- symbol
- half_life_sec
- decay_1 (The Decay Modes, the one Collum is for the decay type that occurs the most often)

All the values except decay_1 were not changed in the process,
but i cleaned up the decay types to reduce the number of different types. 
I have only removed some types that had no known probability, had another decay type, and where i could not find any explanation online, all of these types occurred less than 10 Times. 

### Helpful sites
- https://www-nds.iaea.org/relnsd/vcharthtml/decay_libs.html (This is the same site, but this one has a different dataset)
- https://periodictable.com/Isotopes/001.1/index.dm.prod.html
- https://www.nndc.bnl.gov/ensdf/
- https://www-nds.iaea.org/public/ensdf_pgm/
- https://www-nds.iaea.org/amdc/
