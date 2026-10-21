# Dataset Comparison

## 1. Purpose

This document compares candidate datasets for text classification
and speech recognition in the fraud risk assessment application.

The selection is preliminary. Dataset descriptions have been reviewed,
but the files have not yet been downloaded or tested by the team.

## 2. Dataset Comparison

| Dataset | Data and labels | Proposed use | Main limitation |
| --- | --- | --- | --- |
| UCI SMS Spam Collection | English SMS messages labelled as spam or ham (non-spam). | An introductory experiment with TF-IDF and Logistic Regression. | Spam labels do not directly represent fraud. |
| MeAJOR Corpus | Phishing and legitimate emails collected from multiple sources. | A candidate dataset for phishing classification experiments. | Emails differ from short messages and spoken conversations. |
| E-PhishLLM | Generated phishing detection examples introduced in the E-PhishGen study. | An additional robustness test using generated emails. | Synthetic examples cannot replace evaluation on real messages. |
| ISSAI Kazakh Speech Corpus 2 | Kazakh speech recordings with transcriptions. | Evaluation of Kazakh speech-to-text performance. | The corpus does not provide fraud labels. |

## 3. Preliminary Selection

### Text classification

MeAJOR is a candidate for the main phishing classification experiment
because it contains phishing and legitimate emails.

Before selecting it, we must verify access to the text, label definitions,
language coverage, licence conditions, and dataset quality.

An email dataset alone cannot demonstrate that the application works
well on SMS messages or speech transcripts. These input types require
separate evaluation.

UCI SMS Spam Collection can support an introductory spam classification
experiment. Its spam labels must not be renamed as fraud labels
without reviewing and re-annotating the examples.

E-PhishLLM may support an additional robustness test.
Results on generated data will be reported separately from results
on real messages.

### Speech recognition

KSC2 is a candidate for evaluating Kazakh speech recognition.

A speech recognition model will produce a transcript.
The predicted transcript will be compared with the reference transcript.

Separate recordings with fraud-related and non-fraud-related content
are needed to evaluate the complete speech-to-risk pipeline.

## 4. Language Coverage

English is proposed for initial text experiments.

Suitable labelled Russian and Kazakh fraud datasets have not yet
been confirmed in this comparison.

The team must investigate these data sources before promising
Russian and Kazakh fraud detection support.

Translated examples may help training, but they will not replace
an independent test set of messages originally written in the
target language.

## 5. Checks Before Dataset Approval

For each dataset, we will record:

- The original source and downloaded version.
- The licence and permitted uses.
- Available languages and data fields.
- The number of examples in each class.
- Label definitions and annotation methods.
- Missing text, incorrect labels, and duplicate examples.
- Whether personal information requires removal.
- Relevance to the selected fraud scenarios.

Public availability will not be treated as permission
to redistribute a dataset.

## 6. Preprocessing and Data Splitting

The planned preparation steps are:

1. Inspect text fields, labels, and missing values.
2. Remove unusable records and investigate inconsistent labels.
3. Detect exact duplicates and near-duplicate message templates.
4. Keep related examples in the same data split.
5. Create training, validation, and test sets.
6. Fit text preprocessing and TF-IDF only on the training set.
7. Use validation data for model and threshold selection.
8. Keep test data separate until the final evaluation.

Where possible, an additional test will use a different data source
to examine performance on unfamiliar messages.

Class weighting or resampling will be applied only to training data.

## 7. Current Limitations

The candidate datasets do not yet cover all proposed fraud scenarios,
languages, and input types.

Phishing email results will not be presented as evidence of detecting
every type of fraud.

The final dataset choice will follow a data audit and discussion
with the team and supervisor.

## 8. Sources

1. UCI SMS Spam Collection:
   https://archive.ics.uci.edu/dataset/228/sms+spam+collection

2. Mendes et al. (2025). MeAJOR Corpus:
   A Multi-Source Dataset for Phishing Email Detection.
   https://arxiv.org/abs/2507.17978

3. Pajola et al. (2025). E-PhishGen:
   Unlocking Novel Research in Phishing Email Detection.
   https://arxiv.org/abs/2509.01791

4. ISSAI Kazakh Speech Corpus 2:
   https://issai.nu.edu.kz/kz-speech-corpus/