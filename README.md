# Segmentation Strategies

- Presentation containing all BLEU scores and additional graphs: https://docs.google.com/presentation/d/1WqdPUqvJ0g0qn6PVGymANBHndMhTnmZ1AXZiSIEHcNo/edit?usp=sharing

- VAD Toolkit_1: https://github.com/NickWilkinson37/voxseg

- VAD Toolkit_2: https://github.com/ina-foss/inaSpeechSegmenter

- VAD Toolkit_3: https://github.com/wiseman/py-webrtcvad

- mTEDx test and validation corpora: http://www.openslr.org/100

- Kaldi toolkit: https://github.com/kaldi-asr/kaldi

- Machine translation and speech recognition/translation was done by employing the framework https://github.com/nlp-dke/NMTGMinor

Manual Segmentations and reference translations can be found in the corresponding sets.
The segmentations were performed using the three mentioned toolkits on a local machine. Next, the extraction of the MFCC features was performed on the same local machine by using the Kaldi toolkit. The resulting features (representing all the different segmentations) were uploaded on Google Drive. Then, through a GPU Hardware-accelerated Google Colab session,  the cascaded end-to-end and cascaded were employed for each segmentation.

---
## Results

### Dominating segmentation strategy employing the end-to-end translation model
|   <br>  <br> Language  <br> pair  | Best  <br> segmentation                                        | Segments <br> count       | Segments <br> Difference\*    | BLEU score  <br> Difference\*  |
| :-------------------------------: | :------------------------------------------------------------: | :-----------------------: | :---------------------------: | :----------------------------: |
| pt-es\_test                        | voxseg -s 0\.90                                                | 1294                      | 23\.5%                        | 17\.7%                         |
| pt-es\_valid                       | voxseg -s 0\.95                                                | 1139                      | 11\.7%                        | 18\.1%                         |
| it-en\_test                        | voxseg -s 0\.95                                                | 1223                      | 22\.2%                        | 14\.9%                         |
| it-en\_valid                       | webrtcvad -p 2                                                 | 1075                      | 14\.4%                        | 9\.8%                          |
| it-es\_test                        | voxseg -s 0\.95 <br> inaspeech -r 0.15 <br> inaspeech -r 0.20  | 1223 <br> 1228 <br> 1335  | 22\.2% <br> 22.6% <br> 30.8%  | 15\.9%                         |
| it-es\_valid                       | webrtcvad -p 2                                                 | 1075                      | 14\.4%                        | 11\.7%                         |
| es-en\_test                        | webrtcvad -p 0                                                 | 1116                      | 11\.4%                        | 6\.5%                          |
| es-en\_valid                       | webrtcvad -p 0 <br> webrtcvad -p 1                             | 1082 <br> 1117            | 11\.4% <br> 14.6% <br>        | 9\.5%                          |
| pt-en\_test                        | voxseg -s 0\.90                                                | 1294                      | 23\.5%                        | 15\.1%                         |
| pt-en\_valid                       | voxseg -s 0\.95 <br> inaspeech -r 0.05 <br>                    | 1139 <br> 1199 <br>       | 11\.7% <br> 16.8% <br>        | 16\.5%                         |


Table displaying the best-found segmentation toolkit, the corresponding parameter, and the number of segments created. *The table also shows the percentage difference in segments counts and BLEU score compared to the scores given by the end-to-end translation model when utilizing the manual segmentation

### Dominating segmentation strategy when employing the cascaded translation model

|   <br>  <br>  <br> Language  <br> pair  | Best  <br> segmentation                          | Segments <br> count  | Segments <br> Difference\*  | BLEU score  <br> Difference\*  |
| :-------------------------------------: | :----------------------------------------------: | :------------------: | :-------------------------: | :----------------------------: |
| pt-es\_test                             | voxseg -s 0\.90                                  | 1294                 | 23\.5%                      | 19\.3%                         |
| pt-es\_valid                            | inaspeech -r 0\.05                               | 1199                 | 16\.8%                      | 19\.0%                         |
| it-en\_test                             | inaspeech -r 0\.15 <br> inaspeech -r 0.20 <br>   | 1228  <br> 1335      | 22\.6% <br> 30.8% <br>      | 13\.1%                         |
| it-en\_valid                            | webrtcvad -p 2                                   | 1075                 | 14\.4%                      | 11\.0%                         |
| it-es\_test                             | inaspeech -r 0\.15                               | 1228                 | 22\.6%                      | 16\.6%                         |
| it-es\_valid                            | voxseg -s 0\.90 <br> webrtcvad -p 2              | 991 <br> 1075        | 6\.2% <br> 14.4%            | 12\.8%                         |
| es-en\_test                             | webrtcvad -p 0                                   | 1116                 | 11\.4%                      | 6\.0%                          |
| es-en\_valid                            | webrtcvad -p 1                                   | 1117                 | 14\.6%                      | 7\.7%                          |
| pt-en\_test                             | voxseg -s 0\.90                                  | 1294                 | 23\.5%                      | 16\.6%                         |
| pt-en\_valid                            | inaspeech -r 0\.05                               | 1199                 | 16\.8%                      | 17\.4%                         |


Table displaying the best-found segmentation toolkit, the corresponding parameter, and the number of segments created. *The table also shows the percentage difference in segments counts and BLEU score compared to the scores given by the cascaded translation model when utilizing the manual segmentation.

|   <br> Segmentation <br> strategy  | BLEU scores and \#segments counts <br> on E2E and Cascaded models  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
| :--------------------------------: | :----------------------------------------------------------------: | :---- | :---: | :---: | :---- | :---: | :---- | :---- | :---- | :---: | :---: | :---: | :---: | :---: | :---: |
| Test set                           | pt-es                                                              |       |       | pt-en |       |       | it-en |       |       | it-es |       |       | es-en |       |       |
|                                    | E2E                                                                | \#seg | Casc. | E2E   | \#seg | Casc. | E2E   | \#seg | Casc. | E2E   | \#seg | Casc  | E2E   | \#seg | Casc. |
| voxseg -s 0\.90                    | 32\.9                                                              | 1294  | 32\.3 | 29\.4 | 1294  | 29\.3 | 25\.9 | 998   | 25\.0 | 29\.5 | 998   | 27\.7 | 37\.8 | 1110  | 39\.2 |
| voxseg -s 0\.95                    | 30\.9                                                              | 1602  | 30\.6 | 28\.2 | 1602  | 28\.0 | 26\.7 | 1223  | 25\.5 | 30\.2 | 1223  | 27\.9 | 36\.6 | 1369  | 38\.3 |
| inaspeech -r 0\.05                 | 28\.7 <br>                                                         | 977   | 28\.6 | 25\.7 | 977   | 26\.1 | 23\.6 | 902   | 23\.6 | 27\.1 | 902   | 25\.6 | 38\.4 | 1288  | 39\.5 |
| inaspeech -r 0\.15                 | 31\.6                                                              | 1478  | 31\.1 | 27\.8 | 1478  | 28\.3 | 26\.2 | 1228  | 25\.7 | 30\.2 | 1228  | 28\.1 | 36\.8 | 1574  | 38\.3 |
| webrtcvad -p 2                     | 31\.7                                                              | 1142  | 31\.1 | 27\.6 | 1142  | 27\.7 | 25\.6 | 932   | 
24\.5 | 29\.0 | 932   | 26\.8 | 37\.3 | 1440  | 39\.3 |



Table displaying the BLEU scores and the corresponding number of segments on the Portuguese-Spanish, Portuguese-English, Italian-English, Italian-Spanish, and Spanish-English language pairs when employing five of the most dominating segmentation strategies and both the end-to-end and cascaded models.
