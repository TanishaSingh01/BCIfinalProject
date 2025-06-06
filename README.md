# An EEG Recordings Dataset for Mental Stress Detection
## Description and Quality Evaluation

## Data Description

### Overview
This dataset comprises EEG recordings collected using the EMOTIV EEG 5-Channel Sensor Kit during five distinct types of mental stimulation aimed at inducing or reducing stress. The study investigates the neural correlates of mental stress and contributes to the development of stress detection models based on EEG data.

### Experimental Design/Paradigm
- **Design:** Within-subjects
- **Participants:** 20–22 individuals per task type
- **Total sessions:** 42 sessions
- **Task Types:**
  - Horror Video Stimulation
  - Listening to Relaxing Music
- **Protocol Summary:**
  Each participant was exposed to one or more of the above conditions. EEG data were collected during exposure to stress-inducing and relaxing stimuli. The tasks were selected to provoke varying degrees of cognitive and emotional stress, allowing comparisons across conditions.

### Procedure for Collecting Data
- **Participant Setup:** Participants were seated comfortably and exposed to visual and/or auditory stimuli depending on the condition.
- **Instructions:** Participants were asked to engage fully with each stimulus type (e.g., solve math problems, watch horror clips, relax to music).
- **Data Recorded:** EEG data across 5 channels, with different conditions aimed at eliciting varied mental stress responses.
- **Trial Phases:**
  - Baseline rest period
  - Task/stimulation period

### Hardware and Software Used
- **EEG Hardware:** EMOTIV EEG 5-Channel Sensor Kit
- **Channels:** 5 (AF3, AF4, T7, T8, Pz)
- **Sampling Rate:** 128 Hz
- **Band-Pass Filter:** 1–50 Hz
- **Software Used:** EMOTIVPRO

### Data Size
- **Participants:** 22–24 subjects depending on task
- **Files:** Data organised by task folder (CMPS, TMCT, SCWT, Horror, Relaxing Music)
- **Total Size:** 49.5 MB
- **Total Duration per Session:** 00:02:59

### Number of Channels
- **EEG:** 5 channels (EMOTIV sensor layout)
- **Other Signals:** Not applicable

### Sampling Rate
- **EEG:** 128 Hz
- **Other Signals:** Not applicable

### Data Source and Ownership
- **Website:** https://data.mendeley.com/datasets/wnshbvdxs2/1, Mendeley Data
- **Owner:** Bharati Vidyapeeth Deemed University College of Engineering, Pune
- **Source:** Participants recruited via internal university outreach and voluntary participation
- **Selection Criteria:** Not Specified.
- **Ethics:** Informed consent obtained; study approved by CC BY 4.0 license (The files associated with this dataset are licensed under a Creative Commons Attribution 4.0 International license.

## Usage

### Pip Installs
```bash
!pip install mne
!pip install autoreject
!pip install mne mne-icalabel
```

### Instructions
1. The code is recommended to run in Google Colab
2. Download the EEG dataset from here: An EEG Recordings Dataset for Mental Stress Detection
3. Put the dataset, .ipynb and .py files into the same folder.
4. Change FILE_PATH to the relative path of the downloaded EEG dataset in Google Drive.

## Introduction
Stress is a pervasive condition that affects cognitive performance, emotional well-being, and physical health. Traditional stress management techniques often rely on medication or generalized behavioral therapies, which may not adapt in real time to an individual's mental state. Brain-Computer Interface (BCI) technologies, particularly those utilizing electroencephalography (EEG), offer a promising alternative by enabling the direct interpretation of brain activity for personalized feedback.

This project proposes the design and development of a real-time EEG-based neurofeedback system for stress detection and reduction. By leveraging a publicly available dataset and consumer-grade EEG hardware, the system aims to classify stress levels based on neural responses to various cognitive and emotional stimuli. Using machine learning and signal processing techniques, the project simulates a feedback loop that could guide users toward emotional self-regulation. This research not only addresses the growing need for accessible mental wellness tools but also highlights the potential of open-source data and wearable technology in next-generation healthcare applications.

## Model Framework

![Model Framework - visual selection](https://github.com/user-attachments/assets/999cf5a3-dcdf-4143-8cb9-a0b4d750b971)


### Analysing the Hidden Independent Components within EEG Using ICA with ICLabel

| Component | EEG (5 channel dataset) | Bandpass | Autoreject | Brain | Muscle | Eye | Heart | Line_noise | Channel_noise | Other |
|-----------|-------------------------|----------|------------|-------|--------|-----|-------|------------|---------------|-------|
| Filtered  | ✓                      | ✓        | 13         | 0     | 0      | 0   | 0     | 0          | 11            |       |
| Raw       |                        |          | 16         | 0     | 0      | 0   | 0     | 0          | 23            |       |


![page5_img1](https://github.com/user-attachments/assets/bb6df5d2-c15d-4404-97c8-c3200fed7916)


**Tasks:**
- Horror Video Stimulation
- ![page6_img1](https://github.com/user-attachments/assets/9ba861c7-8da1-4ff8-804f-bed2fefb8080)

- Listening to Calm Music
- ![page6_img2](https://github.com/user-attachments/assets/cf212252-5293-4a9d-879f-d1f8545fe214)


- Raw 

![page7_img1](https://github.com/user-attachments/assets/28b032c9-54a2-48bd-90fb-d11393bd01d1)


- Filtered 

![page8_img1](https://github.com/user-attachments/assets/36535b05-2478-4c45-b16d-dded502c5b87)
**Processing Steps:**
- Raw EGG Common Spatial Patterns (CSP)
- Listening to Calm Music
- ![page9_img1](https://github.com/user-attachments/assets/b0723ba7-2ae4-4d5e-99a4-700540e8da28)
- Horror Video Stimulation
-![page9_img2](https://github.com/user-attachments/assets/4c42831c-2630-4e38-a8f7-ec65e71b03c0)

- Filtered EEG Common Spatial Patterns (Autoreject)
- Listening to Calm Music
- ![page9_img3](https://github.com/user-attachments/assets/8e9808e1-96e9-448f-a215-4a7b10906bb5)
- Horror Video Stimulation
- ![page10_img1](https://github.com/user-attachments/assets/3ddb0ee7-fe29-40cd-b745-4b43651f3c50)


![page10_img2](https://github.com/user-attachments/assets/4b1af599-ad23-4020-b7cc-30ebd2e34747)

![page11_img1](https://github.com/user-attachments/assets/6afbac24-eb24-453b-9e46-49cba1d53419)

**Power-spectral-density before and after cleaning**
![page12_img1](https://github.com/user-attachments/assets/c922844d-aece-4551-862c-8c1bf4e333a7)

![page12_img2](https://github.com/user-attachments/assets/f644832a-947f-4dc0-9dcc-0866fd27c47f)



## Validation
To evaluate the trained classifier, we use multiple validation strategies on the dataset to assess its performance in accurately classifying emotional brain states (horror vs. relaxing). Specifically, we apply 3-fold stratified cross-validation, an 80/20 holdout split, and repeated cross-validation across five random seeds to ensure the model's stability. In addition, we perform hyperparameter tuning using GridSearchCV on the XGBoost classifier. To quantify model effectiveness, we analyse standard classification metrics including accuracy, precision, recall, F1-score, and the confusion matrix.

## USAGE
This section outlines the usage of our BCI model for classifying EEG signals under stress-inducing (horror) and relaxing (music) conditions. The code is implemented in Python and is designed to run seamlessly on Google Colab. It can also be adapted for local execution with minor modifications.

### Environment and Dependencies
To execute the code, the following Python libraries are required:
- **mne** – for EEG data handling and signal processing
- **xgboost** – for implementing the XGBoost classifier
- **autoreject** – for artifact correction (optional)
- **scikit-learn** – for classification and evaluation tools
- **numpy, scipy** – for numerical and statistical computations

You can install all necessary packages using:
```bash
pip install mne xgboost autoreject
```

### Dataset Setup
The model requires the following ZIP files, which should be placed in the working directory (e.g., /content/ in Colab):
- Horrer Video Stimulation.zip
- Participants Listening to Relaxing Music.zip

These archives contain EEG recordings in .edf format. The code will automatically extract and organize the data into subdirectories for further processing.

### Configurable Parameters
Users can modify several components of the pipeline, including:
- **File paths:** Adjust the dataset directory if running locally.
- **Channel selection:** Default channels are AF3, AF4, T7, T8, Pz.
- **Frequency range:** Default band-pass filter is 8–30 Hz.
- **Classifier parameters:** Customize Random Forest, XGBoost, or KNN settings.
- **Cross-validation:** Change number of folds or seeds for repeated validation.

All configurable options are clearly marked in the notebook/script and can be adapted to fit alternative datasets or experimental conditions.

### Execution Instructions
1. Upload the EEG dataset ZIP files and the notebook (.ipynb) to the same directory.
2. Run the notebook sequentially:
   - **Step 1:** Extract and load EEG files
   - **Step 2:** Preprocess signals and select valid EEG channels
   - **Step 3:** Extract features (PSD, entropy, Hjorth parameters)
   - **Step 4:** Train the ensemble classifier
   - **Step 5:** Evaluate the model using multiple validation strategies
3. Outputs are printed and visualized directly in the notebook:
   - Accuracy scores from cross-validation and holdout split
   - Confusion matrix and classification report
   - GridSearch results for XGBoost
   - ICA+ICLabel results (if applicable)

This pipeline provides a complete workflow from raw EEG recordings to emotion classification, allowing reproducible results and further extension for future EEG-based BCI applications.

## Results
This section presents a detailed evaluation of our EEG-based BCI system designed to classify stress-related brain states from horror and relaxing stimuli.

### Classifier and Features
We used an ensemble classifier combining Random Forest, XGBoost, and K-Nearest Neighbors. Input features included:
- Mean and variance of Power Spectral Density (PSD)
- Shannon Entropy
- Hjorth Parameters (Activity, Mobility, Complexity)

### Performance Metrics

| Evaluation Method | Accuracy | Precision | Recall | F1-Score |
|-------------------|----------|-----------|--------|----------|
| 3-Fold Stratified Cross-Validation | 0.76 (avg) | – | – | – |
| 80/20 Holdout Evaluation | 0.78 | 0.75 (Relaxing)<br>0.80 (Horror) | 0.75<br>0.80 | 0.75<br>0.80 |
| GridSearchCV (XGBoost tuned) | 0.74 | – | – | – |
| Repeated Stratified K-Fold (5 seeds) | 0.75 (avg) | – | – | – |

### Comparison with Common Preprocessing Pipelines

| Preprocessing Method | Used? | Reason |
|---------------------|-------|--------|
| ICA | ✘ | Not required raw data was clean and did not contain significant artifacts |
| ICLabel + ASR | ✘ | Same as above; professor recommended skipping |
| Auto-Reject | ✘ | Raw data was found stable and artifact-free |

![page16_img1](https://github.com/user-attachments/assets/c52711c0-7817-4be5-8f4d-0a7ec79e4644)



## Quality Evaluation

### Surveying and Analyzing Existing Literature

**Established Protocols:**
- The experimental design involving stress-inducing and relaxation tasks is well-established in cognitive neuroscience and psychophysiological research on emotional regulation
- Similar protocols have been employed in studies on affective neuroscience and stress regulation, reinforcing the reliability of this study's design (e.g., AlZoubi et al., 2012; Menezes et al., 2021).

**Multimodal Psychophysiological Activity:**
- The effective detection and classification of mental stress relies on multimodal psychophysiological responses to specific task events such as problem-solving onset, emotional stimulus presentation, and relaxation periods.
- This approach aligns with established models of event-related emotional regulation, where cognitive and affective processes are dynamically modulated in response to discrete environmental and internal stimuli (e.g., Micoulaud-Franchi et al., 2021).

**EEG Methodology:**
- The use of a 5-channel EEG system to monitor neural activity offers a cost-effective and portable solution for real-time mental state assessment.
- Literature supports the reliability of EMOTIV EEG headsets in emotion and stress detection studies, making them suitable for applied neurofeedback research (e.g., Sharma, Gedeon, & Lal, 2017).

**Signal Processing:**
- The EEG preprocessing pipeline including bandpass filtering, artifact removal using ICA, and segmentation into task-aligned epochs follows established best practices in EEG signal analysis.
- These methods are widely supported in the literature for improving signal quality and enhancing classification accuracy in affective computing applications (e.g., Makeig et al., 2004).

## References
1. AlZoubi, O., Calvo, R. A., & Yin, J. (2012). Detecting natural stress using EEG signals. In International Conference on Brain Informatics (pp. 192–201). Springer. https://doi.org/10.1007/978-3-642-35139-6_20

2. Menezes, M. L., Lopes, F. M., Borges, K. B., & de Souza, R. E. (2021). An EEG-based machine learning approach for real-time stress detection. Computers in Biology and Medicine, 129, 104132. https://doi.org/10.1016/j.compbiomed.2020.104132

3. Sharma, M., Gedeon, T., & Lal, S. K. (2017). Emotion classification using EEG and deep learning. In 2017 International Joint Conference on Neural Networks (IJCNN) (pp. 2746–2753). IEEE. https://doi.org/10.1109/IJCNN.2017.7966162

4. Micoulaud-Franchi, J. A., Jeunet, C., Pelissolo, A., & Ros, T. (2021). EEG neurofeedback for anxiety disorders and post-traumatic stress disorders: A blueprint for a promising brain-based therapy. Current Psychiatry Reports, 23(12), 84. https://doi.org/10.1007/s11920-021-01299-9

5. Makeig, S., Debener, S., Onton, J., & Delorme, A. (2004). Mining event-related brain dynamics. Trends in Cognitive Sciences, 8(5), 204–210. https://doi.org/10.1016/j.tics.2004.03.008

6. Omejc, N., Rojc, B., Battaglini, P. P., & Marusic, U. (2019). Review of the therapeutic neurofeedback method using electroencephalography: EEG Neurofeedback. Bosnian Journal of Basic Medical Sciences, 19(3), 213–220. https://doi.org/10.17305/bjbms.2018.3785




https://github.com/user-attachments/assets/251aa820-69ca-47aa-807d-17c8748d6ea5

