# SpeakerDiarization
Speaker Diarization is the problem of separating speakers in an audio. There could be any number of speakers and final result should state when speaker starts and ends. In this project, we analyze given audio file with 2 channels and 2 speakers (on separate channel). We train Neural Network for learning when a person is speaking. We use different type of Neural Networks specifically,Recurrent Neural Network (RNN) and Convolution Neural Network (CNN) we achieve 92% of accuracy with RNN. 


## Dataset Description
Our dataset contains 37 audio files approximately of 15 minutes each with sampling rate of 44100 samples/second, recorded in 2 channels with exactly 2 speakers on 2 different microphones. Each audio file has been hand annotated for speakers timings. Annotating timing (in seconds) they start and stop speaking. We use this dataset and split in 3 parts for training, validation and testing.


## Preprocessing

### Data Normalization
We perform normalization of audio files after observing recorded audio was not in the same scale. Few audio files were louder than others and normalization can help bring all audio files to same scale.

### Sampling Audio
With frame rate being high, we have a lot of data. To give an example, in a 15 min audio file we get about 40M samples in each channel.  To reduce data without loosing much information, we down sample audio files by every 4 sample.


# Approach 


## Recurrent Neural Network (RNN)

we tried Recurrent Neural Network on the classification problem. The RNN gives us the best result with 3 layers each with 150 Long short-term memory (LSTM) cells. The LSTM in the graph means a LSTM layer which consists of 150 LSTM cells. The output only has one neuron with sigmoid to predict 0 or 1. 


## Convolution Neural Network (CNN)
To apply CNN, we at first compute the spectrogram for each row of the data matrix, then store them into a new file by using pickle. In this way we don’t need to compute spectrogram online and hence can save a lot of training time. Function scipy. signal.spectrogram is used to compute the spectrogram for each segment. The recomputed spectrogram of each segment then is organized to a 3 dimension matrix with shape (number of segments, height, width). For example, the down sampled data matrix of a channel returned by get data has the shape (100, 1102) for a channel with 100 segments, then the shape of recomputed spectrogram matrix is (100,129,4). The number of segments remains the same. The height 129 and width 4 come from using the default parameters of function scipy. signal.spectrogram. Spectrogram matrices are computed and stored by using code in Spectrogram Generator.

