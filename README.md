# viki
Deep Learning for Speaker and Interruption Recognition in Company Meetings

## About
viki is a web app and deep learning system that listens to company meetings and monitors employees speaking habits and tendencies.

![alt tag](https://raw.githubusercontent.com/nicholaslocascio/viki/master/viki_demo.png)

## Technical Approach
### Problem Setup
Our goal is to predict which employee is speaking from just an audio snippet. We use a Deep Recurrent Neural Network Architecture to process the audio to make these predictions. We won't have much have much training data from each employee since it is unreasonable to ask each employee to dictate hours of speech. We are thus restricted to 1 minute of audio from each employee.

### Pre-training & Transfer Learning
To compensate for the lack of employee training data, we pretrain our network on a large dataset of ~1000 hours of speaking from various audiobooks and speakers (from https://librivox.org/). We train the net to classify which speaker the audio snippet belongs to. The net learns much about processing audio and speech invariants to consider. The activations of the last layer before the softmax output contains an extremely relevant vector space representation of the processed audio, akin to the vector representations of the activations of the last 4096 nodes on Alex-Net or VGG that have application in image-related tasks.

### SVM
We use our pre-trained audio-processing neural network to process snippets from the 1 minute of audio from each employee to get a set of continuous vector-representations of each audio sample. We then train an SVM to classify these vectors to their correct employee. When a meeting is ongoing, we similarily pass the audio snippets from the meeting to our trained neural net to get a relevant vector space representation, and then pass this vector to our trained SVM for final classification.

## Note
This project was made for HACKMIT 2015.
It is a bare-bones prototyle built in ~20 hours so please excuse any bad code, organization, and incomplete features.
