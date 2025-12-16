# Macedonian Sign Language Recognition (MSL)

This project implements a real-time **sign language recognition system** for the **Macedonian Sign Language (MSL)** alphabet and some words. It uses **MediaPipe Holistic** for extracting pose, face, and hand landmarks, and a **stacked LSTM model** for sequence classification.  

The system supports:  
- Recording raw sign language samples from webcam  
- Extracting keypoints from face, pose, and hands  
- Data augmentation via transformations (translation, rotation, scaling)  
- Training LSTM models for alphabet and word recognition  
- Real-time sign language recognition from webcam  

---

## Features

- **Data Collection**  
  - Record video samples for each alphabet/word sign.  
  - Save extracted keypoints into `.npy` sequences for training.  

- **Data Augmentation**  
  - Generate variations of recorded signs with translations and rotations.  
  - Expand dataset to improve model generalization.  

- **Model**  
  - Stacked **LSTM (Long Short-Term Memory)** network.  
  - Input shape: `(30 frames, 1662 features)` (pose + face + hands).  
  - Output: classification across 31 alphabet signs or 30 words.  

- **Live Recognition**  
  - Capture video from webcam.  
  - Perform real-time keypoint extraction.  
  - Predict sign sequences and display recognized sign on screen.  

---

## Supported Signs

All signs are based on [Talking Hands](https://znakoven.mk/).

### Macedonian Alphabet
А, Б, В, Г, Д, Ѓ, Е, Ж, З, Ѕ, И, Ј, К, Л, Љ, М, Н, Њ, О, П, Р, С, Т, Ќ, У, Ф, Х, Ц, Ч, Џ, Ш

For reference: [MSL Alphabet](https://znakoven.mk/%d0%b0%d0%b7%d0%b1%d1%83%d0%ba%d0%b0/)

### Words

#### Colors
Добро, Здраво, Како сте, Лошо, Пријатно, Така Така, Бела, Безбојно, Боја, Бои, Жолта, Златна, Кафеава, Месо боја, Плава, Портокалова, Розева, Светла, Сива, Сребро, Темна, Црвена, Црна, Црна (втор знак)  

Reference: [MSL Colors](https://znakoven.mk/%d0%b1%d0%be%d0%b8/)

#### Greetings
Добро, Здраво, Како сте, Лошо, Пријатно, Поздравување, Така Така  

Reference: [MSL Greetings](https://znakoven.mk/%d0%bf%d0%be%d0%b7%d0%b4%d1%80%d0%b0%d0%b2%d1%83%d0%b2%d0%b0%d1%9a%d0%b5/)

#### Technology
Веб страна, Компјутер, Лаптоп, Мобилна мрежа, Рутер  

Reference: [MSL Technology](https://znakoven.mk/%d1%82%d0%b5%d1%85%d0%bd%d0%be%d0%bb%d0%be%d0%b3%d0%b8%d1%98%d0%b0-2/)

---

## Requirements

- Python **3.8+**
- [OpenCV](https://pypi.org/project/opencv-python/)
- [MediaPipe](https://pypi.org/project/mediapipe/)
- [NumPy](https://numpy.org/)
- [TensorFlow / Keras](https://www.tensorflow.org/)

Install all dependencies with:

```bash
pip install numpy==1.26.4
pip install opencv-contrib-python==4.8.1.78
pip install mediapipe 
pip install tensorflow scikit-learn matplotlib
```
---

## Data Collection

Run the script to record samples from your webcam:

- **`s`** → Start recording **30 frames** for the current sign  
- **`n`** → Switch to the **next sign** in the list  
- **`q`** → **Quit** the recording session

---

## Data Augmentation

Generate more samples from recorded videos using transformations (translation, rotation, scaling):

```bash
generate_samples(actions, data_collection_map)
```

This ensures at least 500+ samples per class.

---

## Live Recognition

Run live recognition from webcam:

```bash
live_recognition(model, actions, action_labels)
```

Predictions are displayed in real-time.

Recognized sign labels appear as overlay text.

