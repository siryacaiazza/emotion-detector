# 😄 Emotion Classifier

<div align="center">
An accurate emotion detector for .wav audio files using both state-of-the-arts ResNet18 and a costum build CNN.

[🧾Project Description](#project-description) ● [📊Data](#data) ● [🧩Features](#features) ● [🛠️Installation](#installation) ● [🚀Launching the Dashboard](#launching-the-dashboard)

</div>

## 🧾Project Description

The `EmotionClassifier.ipynb` notebook is designed to:
- Process audio files to extract features relevant for emotion detection.
- Organize audio metadata (emotion, gender) into a pandas DataFrame.
- Visualize audio waveforms, spectrograms, and Mel-frequency cepstral coefficients (MFCCs).
- Use the extracted features to train two different models, one using state-of-the-art ResNet18 and one custom built.
- Test the performance of the models by computing multiple metrics.

**The models are ready to be used by running the `DashboardEmotion.ipynb` code, as explained in the [🚀Launching the Dashboard](#dashboard) section.**

## 📊Data

The data used for this project can be found at this [link](https://www.kaggle.com/datasets/uwrfkaggler/ravdess-emotional-speech-audio).
The data is retrieved from the RAVDESS dataset, which contains full AV files, video-only and audio-only files, both of speech and song. The portion used contains 1440 files, all speech and audio-only: 24 actors (12 males, 12 females) acted different emotion for a total of 60 times each. Speech emotions include calm, happy, sad, angry, fearful, surprise and disgust. Each phrase is produced at two levels of emotional intensity, normal and strong, except for the neutral emotion.
Each audio name consists of a 7 part numerical identifier, which indicate the audio's charateristics:
- **Part 1**: Modality (01 = full-AV, 02 = video-only, 03 = audio-only), the files used are all audio-only.
- **Part 2**: Vocal Channel (01 = speech, 02 = song), the files used are all speech.
- **Part 3**: Emotion (01 = neutral, 02 = calm, 03 = happy, 04 = sad, 05 = angry, 06 = fearful, 07 = disgust, 08 = surprised).
- **Part 4**: Emotional intensity (01 = normal, 02 = strong). There is no strong intensity for the 'neutral' emotion.
- **Part 5**: Statement (01 = "Kids are talking by the door", 02 = "Dogs are sitting by the door").
- **Part 6**: Repetition (01 = 1st repetition, 02 = 2nd repetition).
- **Part 7**: Actor (01 to 24. Odd numbered actors are male, even numbered actors are female).

## 🧩Features

### 🔧Preprocessing of the data
- The filenames are used to create a dataframe which contains all the information of the audio, alongside its name and the path from which it is retrieved.
- The labels used for classification are consituted by both the emotion and the gender of the speaker (example: female_fear, male_sad, etc.), for a total of 14 classes.
- The dataset is then split in train, validation and test. For the train dataset some augmentation (addition of noise and shifting of the audio) are applied.
- Each audio is then transformed to retrieve its MFCC with a number of 40 MFCCS and 194 time frames.
### 🔨Building the models
- The MFCCs are used to train two convolutional neural networks (CNNs), one based on the pretrained ResNet18 and one custom built.
- The ResNet18 is modified in order to process 1-channel MFCCS, its fully connected layer is substituted by an identity layer, average pooling is applied in order to keep temporal information and finally a classification layer is added. (NOTE: the Network was deep enough that some dimension were automatically suppressed, so in the forward method before the average pooling dimension are restored)
- The custom model consists of 18 layers: the idea behind it was to decompose the MFFC image along 512 neurons and then slowly decrease the number in order for the network to be able to learn which part of the image where the most important in classifying the emotion, before the classifying layer temporal pooling is applied to keep the temporal information.

| Model | Number of parameters | Training time | Training epochs |
|-------|----------------------|---------------|-----------------|
| Model ResNet18 | ~11.17M | ~42 minutes | 35 |
| Model Costum CNN | ~10.87M | ~1 h 16 minutes | 62 |

All the training times refer to Colab's T4 GPU.

### ➰Training and Testing 
- For each epoch of the training loop, both train accuracy and loss and validation accuracy and loss were saved and displayed. Earlystopping and dynamic learning rate were implemented to optimize training time and efficiency.
- The models were tested and multiple metrics were computed to assess their performances, the results are shown in the following table. 

|  Model   | Accuracy | F1 (weighted) | F1 (macro) | Precision (weighted) | Precision (macro) | Recall (weighted) | Recall (macro) |
|----------|----------|---------------|------------|----------------------|-------------------|-------------------|----------------|
| Model ResNet18 | 0.788 | 0.787 | 0.779 | 0.797 | 0.792 | 0.788 | 0.779 |
| Model Custom CNN | 0.865 | 0.863 | 0.855 | 0.872 | 0.865 | 0.865 | 0.856 | 

## 🛠️Installation

### 📝Prerequisites

- Google account to use Colab
- Access to Colab's T4 GPU & RAM

### 🔍How to use the code

This project uses a large model file that cannot be stored on GitHub directly, so in order to be able to use the files you must:

1. ➡️ Download the dataset from this [link](https://www.kaggle.com/datasets/uwrfkaggler/ravdess-emotional-speech-audio).
2. ➡️ Download the files of this Github repository and add them to your Drive, alongside the dataset.
3. ➡️ Change path of this line in order to access the files and data where you put them in your Drive:
   ```bash
   %cd '/content/drive/MyDrive/Colab Notebooks/ProgettiEsami/ProjectBigImaging'
   ```
4. ➡️ Remember to put the Emotion Dataset in the same directory as above or else the code will run into problems because of this line:
   ```bash
   root_dir = './Emotions'
   ```
All the needed libraries are already imported, if you want to run this code on your local machine instead of Google Colab, the needed libraries are listed in the `requirements.txt` file.

## 🚀Launching the Dashboard

You can use the `DashboardEmotion.ipynb` jupiter notebook to launch the already trained models for inference on your .wav files:
1. ➡️ Download the models from [Google Drive](https://drive.google.com/drive/folders/1ymERLsYVAziu0meQ8aY08ukcASVVTvTR?usp=sharing).
2. ➡️ Once the models are downloaded, you can open the notebook in Colab, and upload them in the local files:
   - Click on the directory 🗂️ icon on the left.
   - Click on the first icon of the row below "File" (it looks like a paper sheet with and upwards arrow inside).
   - Load the .pth files from your computer (it might take a couple of minutes for them to load completely).
3. ➡️ Run the code: the last cell will output something similar to <NgrokTunnel: "https://02a3543e7ceb.ngrok-free.app" -> "http://localhost:8501">, click on the first link, proceed to the website and you can use the app! \[NOTE: these links are not currently working, you must run the notebook to use the dashboard]


