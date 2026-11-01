# Numbers for the report

## Recordings and original sampling rates

| recording | activity | member | acc_hz_original | gyro_hz_original | acc_unit_original | duration_s |
|---|---|---|---|---|---|---|
| jumping | jumping | Laura Celine | 99.700 | 99.700 | m/s2, gravity removed | 88.900 |
| standing_full | standing | Laura Celine | 99.700 | 99.700 | m/s2, gravity removed | 89.800 |
| still | still | Laura Celine | 99.700 | 99.700 | m/s2, gravity removed | 91.700 |
| walking_full | walking | Laura Celine | 99.700 | 99.700 | m/s2, gravity removed | 94.700 |

All recordings were resampled to a common **50 Hz**.

## Files and seconds per activity

| activity | files | seconds | train_files | test_files | has_90_s |
|---|---|---|---|---|---|
| standing | 17 | 89.900 | 12 | 5 | False |
| walking | 18 | 94.700 | 13 | 5 | True |
| jumping | 17 | 88.900 | 12 | 5 | False |
| still | 18 | 91.700 | 13 | 5 | True |

## Windowing and features

Window 2.0 s (100 samples), hop 0.5 s, FFT resolution 0.50 Hz, 14 features: a_mean, a_std, a_range, a_sma, a_corr_xy, a_corr_xz, a_corr_yz, g_mean, g_std, a_domfreq, a_energy, a_entropy, g_domfreq, g_energy.

## Training

Baum-Welch: 6 iterations, converged by the log-likelihood test: True.

## Evaluation on unseen recordings (Baum-Welch model)

| State (Activity) | Number of samples | Sensitivity | Specificity | Accuracy (one vs rest) |
|---|---|---|---|---|
| standing | 44 | 0.909 | 1.000 | 0.976 |
| walking | 44 | 1.000 | 0.968 | 0.976 |
| jumping | 42 | 1.000 | 1.000 | 1.000 |
| still | 38 | 1.000 | 1.000 | 1.000 |
| Overall | 168 | 0.977 | 0.992 | 0.976 |

## Supervised-only versus Baum-Welch

| model | overall accuracy | mean sensitivity | mean specificity |
|---|---|---|---|
| Baum-Welch | 0.976 | 0.977 | 0.992 |
| Supervised only | 0.976 | 0.977 | 0.992 |

## Transition matrix A

| from \ to | standing | walking | jumping | still |
|---|---|---|---|---|
| standing | 0.870 | 0.033 | 0.027 | 0.070 |
| walking | 0.038 | 0.905 | 0.036 | 0.021 |
| jumping | 0.029 | 0.034 | 0.901 | 0.036 |
| still | 0.034 | 0.055 | 0.020 | 0.891 |

## Links

# Links for the report

Repository: https://github.com/62laura/hmm-activity-recognition

- Video, standing: https://github.com/62laura/hmm-activity-recognition/blob/main/videos/evidence/standing.mp4
- Video, walking: https://github.com/62laura/hmm-activity-recognition/blob/main/videos/evidence/walking.mp4
- Video, jumping: https://github.com/62laura/hmm-activity-recognition/blob/main/videos/evidence/jumping.mp4
- Video, still: https://github.com/62laura/hmm-activity-recognition/blob/main/videos/evidence/still.mp4
- Report file: not uploaded yet
