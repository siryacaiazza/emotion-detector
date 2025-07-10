# 😄 Emotion Detector & CLassifier

<div align="center">
An accurate emotion detector for .wav audio files using both state-of-the-arts ResNet18 and a costum build CNN.

[🧩Features](#features) ● [📊Data](#data) ● [🛠️Installation](#installation) ● [📝Usage](#usage) ● [🚀Launching the Dashboard](#dashboard) ● [📚Libraries Used](#libraries-used)

</div>

## Project Description

The `EmotionDetector.ipynb` notebook is designed to:
- Process audio files to extract features relevant for emotion detection.
- Organize audio metadata (emotion, gender) into a pandas DataFrame.
- Visualize audio waveforms, spectrograms, and Mel-frequency cepstral coefficients (MFCCs).

## Setup

To run this notebook, you will need to have the following libraries installed:

```bash
pip install torch pandas librosa matplotlib seaborn scikit-learn
## 🔗 Download Model File

This project uses a large model file that cannot be stored on GitHub directly.

➡️ [Download the model from Google Drive](https://drive.google.com/drive/folders/1ymERLsYVAziu0meQ8aY08ukcASVVTvTR?usp=sharing)

## Launch The Dashboard

You can use the "DashboardEmotion.ipynb" jupiter notebook to launch the models. In order for the dashboard to work properly, once the models have been successfully downloaded, they need to be uploaded in the "/content" directory of Google Colab, you can do so by opening the notebook, clicking on the directory icon on the left, and click on the first icon of the row below "File". Once the model are uploaded completely (this might take a few minutes), you can run the code. 
The last cell will output something similar to <NgrokTunnel: "https://02a3543e7ceb.ngrok-free.app" -> "http://localhost:8501">, click on the first link and you can use the app!

