# Human Activity Recognition with a Hidden Markov Model


A Hidden Markov Model written from scratch with numpy recognises four activities (standing, walking, jumping, still) from smartphone accelerometer and gyroscope recordings.

## Submission links

- Evidence video, standing: https://github.com/62laura/hmm-activity-recognition/blob/main/videos/evidence/standing.mp4
- Evidence video, walking: https://github.com/62laura/hmm-activity-recognition/blob/main/videos/evidence/walking.mp4
- Evidence video, jumping: https://github.com/62laura/hmm-activity-recognition/blob/main/videos/evidence/jumping.mp4
- Evidence video, still: https://github.com/62laura/hmm-activity-recognition/blob/main/videos/evidence/still.mp4

## Data

- Recorded with the Sensor Logger app (accelerometer and gyroscope).
- 70 labelled CSV files of 5 to 10 seconds in `data/segments/`, each with a `timestamp_s` column, resampled to 50 Hz.
- Recordings were split by recording into training and unseen test data, so no test recording was used for training.

| activity | files | seconds | train_files | test_files | has_90_s |
|---|---|---|---|---|---|
| standing | 17 | 89.900 | 12 | 5 | False |
| walking | 18 | 94.700 | 13 | 5 | True |
| jumping | 17 | 88.900 | 12 | 5 | False |
| still | 18 | 91.700 | 13 | 5 | True |

## Method

- Windows of 2.0 s with 0.5 s hop. 14 time-domain and FFT features per window, z-scored with training statistics only.
- Gaussian HMM (diagonal covariance) in numpy: forward-backward, Viterbi decoding, Baum-Welch with a log-likelihood convergence check. Initialised from the labelled training windows.

## Results on unseen recordings

| State (Activity) | Number of samples | Sensitivity | Specificity | Accuracy (one vs rest) |
|---|---|---|---|---|
| standing | 44 | 0.909 | 1.000 | 0.976 |
| walking | 44 | 1.000 | 0.968 | 0.976 |
| jumping | 42 | 1.000 | 1.000 | 1.000 |
| still | 38 | 1.000 | 1.000 | 1.000 |
| Overall | 168 | 0.977 | 0.992 | 0.976 |

## Repository layout

```
data/segments/   labelled CSV files
data/features/   windows and features, scaler
notebooks/       01 to 05, run in order in Google Colab
models/          trained HMM parameters
figures/         plots used in the report
results/         metrics and tables
videos/evidence/ the 4 evidence videos
reports/         the report
```

## How to reproduce

Run the notebooks in `notebooks/` in order (1 to 4) in Google Colab. They ask for your GitHub details and upload steps are described inside each notebook.

## Limitations

- One participant and one phone, and a small amount of data per activity.
- Training sessions for the transition matrix are built by chaining recordings of single activities, so the off-diagonal probabilities are a modelling choice and not natural behaviour.
