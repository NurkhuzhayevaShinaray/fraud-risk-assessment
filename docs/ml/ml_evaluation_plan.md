# ML and Speech Evaluation Plan

## 1. Purpose

This document describes how the text and speech components
will be evaluated.

The evaluation will compare two text classification approaches,
measure speech recognition quality, and examine how transcription
errors affect fraud risk assessment.

This is a plan. No experimental results are claimed.

## 2. Models to Compare

| Approach | Method | Purpose |
| --- | --- | --- |
| Baseline | TF-IDF with Logistic Regression | Provide a simple and reproducible reference. |
| Modern approach | Fine-tuned XLM-R | Evaluate whether contextual multilingual representations improve classification. |

Both models will use the same labelled examples and data splits.

The positive class will represent fraud-related content
according to the agreed annotation guidelines.

Spam labels will not automatically be treated as fraud labels.

## 3. Dataset Preparation

Before training, we will:

- Verify dataset sources, licences, languages, and label meanings.
- Remove unusable records.
- Investigate inconsistent labels.
- Identify exact duplicates and related message templates.
- Record the number of examples in each class and language.

Related examples, including translations and paraphrases,
must remain in the same split to reduce data leakage.

## 4. Training and Test Design

The proposed split is:

- 70% for training.
- 15% for validation.
- 15% for testing.

These proportions may be adjusted after the data audit.
Existing reliable dataset splits will be considered first.

Class proportions will be preserved where possible without
separating related examples across splits.

Training data will be used to fit preprocessing and models.
Validation data will be used to select settings and thresholds.
Test data will remain untouched until these choices are fixed.

We will save split identifiers and random seeds.

Where possible, a separate data source will be used
to test generalisation to unfamiliar messages.

## 5. Class Imbalance

The number of fraud-related and non-fraud-related examples
may differ substantially.

We will compare ordinary training with class-weighted training.
Any resampling will be applied only to the training set.

Validation and test sets will not be artificially balanced.
Their class distributions will be reported.

## 6. Text Classification Metrics

| Metric | Evaluation question |
| --- | --- |
| Precision | Of the messages flagged as fraud-related, how many have the positive reference label? |
| Recall | Of all positively labelled messages, how many did the model detect? |
| F1 | How well does the model balance Precision and Recall? |
| ROC-AUC | How well do prediction scores rank positive examples above negative examples across thresholds? |

ROC-AUC will be calculated from continuous prediction scores,
not from final class labels.

We will also report:

- A confusion matrix with error counts.
- Average Precision as an additional measure for imbalanced data.
- Results by language and input type where sufficient data exist.
- The number of evaluated examples in each group.
- Inference time and the hardware used.

## 7. Error Analysis

We will review false positives and false negatives.

False positive:
A legitimate message is incorrectly flagged as fraud-related.

False negative:
A fraud-related message is incorrectly classified as non-fraud-related.

The review will examine possible causes, including:

- Legitimate requests containing urgent language.
- Fraud without obvious warning words.
- Short messages with insufficient context.
- Spelling variations and unfamiliar wording.
- Language mixing.
- Speech transcription errors.

Examples used in reports will be anonymised where necessary.

## 8. Speech Evaluation

The initial speech-to-text candidate is Whisper.

For each evaluated recording, we need:

- The audio.
- A manually checked reference transcript.
- A language label.
- A fraud-related or non-fraud-related label for end-to-end testing.

General speech corpora can evaluate transcription,
but cannot evaluate fraud detection without suitable labels.

Speech recognition will be measured using Word Error Rate:

WER = (substitutions + deletions + insertions) / reference words

Lower WER indicates fewer word-level transcription errors.

The text normalisation rules used for WER will be documented.

We will compare fraud classification using:

1. The reference transcript.
2. The transcript produced by the speech recognition model.

This comparison will show how transcription errors affect
Precision, Recall, and F1.

Clean audio, noisy audio, and mixed-language recordings
will be evaluated separately where data are available.

## 9. Risk Score and Risk Levels

The application will display a Risk Score from 0 to 100.

The proposed score is 100 multiplied by the model's estimated
positive-class probability after calibration has been evaluated.

Calibration will be fitted using held-out training data
or cross-validation within the training set.
The final test set will not be used for calibration.

We will inspect calibration curves and the Brier score.

Two thresholds will define the risk levels:

- Low: score below the lower threshold.
- Medium: score from the lower threshold up to the upper threshold.
- High: score at or above the upper threshold.

Thresholds will be chosen using validation data and the
agreed trade-off between missed fraud and false alarms.

The score represents a model assessment within the evaluated
task. It is not proof of fraud or a guaranteed real-world probability.

## 10. Model Selection and Export

The final model will be selected using validation results,
including F1, Precision, Recall, inference time, and resource use.

The modern model will not be selected automatically.
The baseline may be preferred if it offers a better practical balance.

After selection, the fixed model will be evaluated on the test set.

The exported package will include:

- The trained model.
- Its vectorizer or tokenizer.
- The label mapping.
- Any calibration component.
- The selected decision and risk thresholds.
- Dependency versions.
- A model version and limitations document.

Predictions will be checked before and after reloading
the exported package.

## 11. Completion Criteria

The evaluation work will be considered complete when:

- Both approaches have been compared on the same test partition.
- Required metrics and class counts have been reported.
- False positives and false negatives have been analysed.
- Speech recognition and end-to-end results have been reported.
- Risk thresholds and their selection method have been documented.
- The exported model can be reloaded successfully.
- Limitations and unsupported scenarios have been recorded.

Numerical performance targets will be agreed with the supervisor
after the data audit and before final test evaluation.
They are not yet approved requirements.

## 12. Reproducibility

Each experiment will record:

- Dataset version and split identifiers.
- Code commit.
- Preprocessing settings.
- Model settings and random seeds.
- Software versions and hardware.
- Evaluation results.

This information will allow the team to repeat and inspect
the experiments.