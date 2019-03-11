### Unsupervised Feature Learning Based on Deep Models for Environmental Audio tagging
Mathis Petrovich



### What is environmental audio tagging?
- Input: Environmental audio
- Output: A label (= a tag) for each acoustic event
  - Or multilabel on a audio chunk



### Dataset used for this problem
- Part of the challenge:
  - Detection and Classification of Acoustic Scenes and Events 2016 (DCASE) $[11]$
- Based on the CHiME-home dataset $[20]$


### Dataset used for this problemls
- $4$ seconds chunks (at $16$ kHz)
- $4378$ chunks in total
  - $1946$ available for training
  - $816$ for evaluation in the challenge


### Dataset used for this problemls
<image src="images/chimie.png" controls style="width:100%"></image> 


### Dataset used for this problemls
CR_lounge_200110_1601.s1200_chunk42.16kHz
<audio src="sounds/CR_lounge_200110_1601.s1200_chunk42.16kHz.wav" controls style="width:100%"></audio> 
- Majority vote: cfv 
  - child
  - adult female
  - video game/TV



## Unsupervised feature learning ?
- Extract features from unlabeled data
- Learned them with a network



## Context of this problem
- A lot of data in the Internet with tags. (YouTube videos etc)
- But very noisy ☹
  - Multiple source
  - Background noise
  - etc

$\Rightarrow$ need a good feature representation



## Traditional methods
<!-- -- data-background-color="#A0C66B" data-background-transition="linear" -->



## Some ideas
low level acoustic features $\Rightarrow$ "bag of audio words"
- KMeans clustering $[5]$-$[9]$
- Gaussian mixtures (GMM) $[9]$
- SVM methods $[12]$



## Deep learning methods
Learn a representation of the data $[13]$-$[17]$

Better performance but:
- input features?
- objective functions?
- not rebust yet



## Solutions of the article
<!-- -- data-background-color="#A06BC6" data-background-transition="linear" -->



## Using DNN nets
<image src="images/dnn.png" controls style="width:100%"></image> 


## Training
- Use binary cross-entropy loss
$- \sum_{i} \left[ y_i \log(\text{pred}_i) + (1 - y_i) \log (1-\text{pred}_i) \right]$


## Pros
- Reduce model size
- Training/testing time reduced
- Serve as a deep PCA framework


## Cons
- Problem with background noise
- Overfitting on the training set



## Solutions 



### Background noise aware training
- Estimate noise at each frames
- Extend features with them



## Using dropout
- In training for earch iteration
  - Remove with probabiliy $p$ a unit
- In testing (like a model averaging process)
  - Scale parameters ($(1-p)$) factor)
  - Feed the network



## Creating data-driven learned features
<!-- -- data-background-color="#C6A06B" data-background-transition="linear" -->



## Mel filter banks
<image src="images/mel.png" controls style="width:100%"></image> 


## MFCCs
Apply a Discrete Cosine Transform (DCT) on MFBs.
- Compressed representation
- Can discard informations



## Auto encoder stucture (DAE)
<image src="images/vae.png" controls style="width:100%"></image> 


## Motivation
- Training with unlabeled data
- Compact representation needed
  - (chunk level labels)
  



## Final network (asyDAE)
<image src="images/asyDAE.png" controls style="width:100%"></image> 




## Preproces the input features
- Compute 40-dimension logarithmic MFBs 
- Extend with the background noise vector
- Normalize (zero mean, unit variance)



## Results
<!-- -- data-background-color="#6BC6A0" data-background-transition="linear" -->



## EER metric
In the graph FPR ($x$-axis)/TPR($y$-axis)

Value of $x$ when $x + y = 1$



### Results (on the evaluation set)
|            | EER     |
|------------|---------|
| MFCC-DNN   | $0.168$ |
| MFB-DNN    | $0.157$ |
| syDAE-DNN  | $0.153$ |
| asyDAE-DNN | $0.148$ |


### Conlusion of this article
Major contributions in audio tagging
- Better acoustic modeling
- Better feature learning



## Personal contribution
<!-- -- data-background-color="#6BA0C6" data-background-transition="linear" -->



### Find source code on gihub
<image src="images/readme.png" controls style="width:100%"></image> 



## Fail to make it work
- A lot of files are missing
- Not designed to be usable
  - No comments/documentation
  - No explaination/readme


## Fail to make it work
<image src="images/errorE.png" controls style="width:50%"></image> 

Missing files
<image src="images/error.png" controls style="width:100%"></image> 



### Huge thanks to this repo
<image src="images/repo.png" controls style="width:100%"></image> 



### Recreate experiment with MFBs
- Train the DAE model to output "good" features
- Train the DNN model with MFBs (problems with the DAE features)


## Graph of DAE autoencoder
<image src="images/dae_graph.png" controls style="width:33%"></image>



## EER results
| c     | m     | f     | v     | p     | b     | o     | avg   |
|-------|-------|-------|-------|-------|-------|-------|-------|
| 0.192 | 0.265 | 0.315 | 0.008 | 0.208 | 0.000 | 0.319 | 0.187 |


## Precisison results
| c     | m     | f     | v     | p     | b     | o     | avg   |
|-------|-------|-------|-------|-------|-------|-------|-------|
| 0.700 | 0.667 | 0.310 | 1.000 | 0.757 | 1.000 | 0.645 | 0.780 |


## Recall results
| c     | m     | f     | v    | p     | b     | o     | avg   |
|-------|-------|-------|------|-------|-------|-------|-------|
| 0.928 | 0.176 | 0.391 | 0.98 | 0.750 | 0.250 | 0.278 | 0.744 |


## Fvalue results
| c     | m     | f     | v     | p     | b     | o     | avg   |
|-------|-------|-------|-------|-------|-------|-------|-------|
| 0.797 | 0.279 | 0.346 | 0.993 | 0.753 | 0.400 | 0.388 | 0.762 |



## Conclusion
- New ideas in the domain
- Inspire other article
- Implementation/reproducibily of results 
  - not easy



## Reference
- Same as the article
