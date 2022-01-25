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
