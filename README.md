# Segmentation Strategies

This project consisted of comparing three popular VAD toolkits and understanding the outcome of applying automatic segmentations on a state-of-the-art multilanguage translation model compared to a cascaded one.

![Screenshot](ted_banner.jpg)

- Presentation containing all BLEU scores and additional graphs: https://docs.google.com/presentation/d/1WqdPUqvJ0g0qn6PVGymANBHndMhTnmZ1AXZiSIEHcNo/edit?usp=sharing

- VAD Toolkit_1: https://github.com/NickWilkinson37/voxseg

- VAD Toolkit_2: https://github.com/ina-foss/inaSpeechSegmenter

- VAD Toolkit_3: https://github.com/wiseman/py-webrtcvad

- mTEDx test and validation corpora: http://www.openslr.org/100

- Kaldi toolkit: https://github.com/kaldi-asr/kaldi

- Machine translation and speech recognition/translation was done by employing the framework: https://github.com/nlp-dke/NMTGMinor

- The end-to-end and cascaded multilingual translation models: https://aclanthology.org/2021.iwslt-1.15/

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
