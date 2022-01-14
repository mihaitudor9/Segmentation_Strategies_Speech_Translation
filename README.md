# Segmentation Strategies

##B.A. thesis - Maastricht University

###Department of Data Science and Knowledge Engineering

###Mihai-Andrei Tudor

Presentation containing all BLEU scores and additional graphs: https://docs.google.com/presentation/d/1WqdPUqvJ0g0qn6PVGymANBHndMhTnmZ1AXZiSIEHcNo/edit?usp=sharing

Toolkit_1: https://github.com/NickWilkinson37/voxseg

Toolkit_2: https://github.com/ina-foss/inaSpeechSegmenter

Toolkit_3: https://github.com/wiseman/py-webrtcvad

mTEDx test and validation corpora: http://www.openslr.org/100

kaldi toolkit: https://github.com/kaldi-asr/kaldi

Machine translation and speech recognition/translation was done by employing the framework https://github.com/nlp-dke/NMTGMinor

Manual Segmentations and reference translations can be found in the corresponding sets.
The segmentations were performed using the three mentioned toolkits on a local machine. Next, the extraction of the MFCC features was performed on the same local machine by using the Kaldi toolkit. The resulting features (representing all the different segmentations) were uploaded on Google Drive. Then, through a GPU Hardware-accelerated Google Colab session,  the cascaded end-to-end and cascaded were employed for each segmentation.
