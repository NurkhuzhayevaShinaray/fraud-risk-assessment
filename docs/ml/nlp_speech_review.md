# Preliminary NLP and Speech Literature Review

## 1. Purpose

This review examines research relevant to fraud risk assessment
using text and speech.

The application will convert speech into text and analyse
the resulting transcript with a text classifier.

The review supports the selection of models, datasets,
and evaluation methods. It is based on an initial review
of the publications and will be expanded during development.

## 2. Text Classification Research

### 2.1 Cross-lingual Representation Learning

Conneau et al. (2020) introduced XLM-R, a multilingual
language model.

Relevance:
XLM-R is a candidate for the modern text classification
approach in our project.

Limitation:
A multilingual model is not automatically a fraud detector.
It requires task-specific training and separate evaluation
for each target language.

Project implication:
Compare a fine-tuned XLM-R model with a TF-IDF and
Logistic Regression baseline.

### 2.2 Phishing Detection Using Textual Signals

Paul et al. (2024) investigated phishing detection as an NLP
task and introduced annotations based on phishing signals.

Relevance:
The study supports examining the content of messages
and defining clear annotation guidelines.

Limitation:
The study focuses on emails. Its findings do not directly
establish performance on SMS messages or speech transcripts.

Project implication:
Document the meaning of each label and examine which
message characteristics lead to classification errors.

### 2.3 MeAJOR Corpus

Mendes et al. (2025) introduced a dataset combining phishing
and legitimate emails from multiple sources. The study
evaluated classification models with different feature sets.

Relevance:
The corpus is a candidate source for phishing experiments.

Limitation:
The published results use the authors' data preparation,
features, and evaluation conditions. They are not expected
results for our application.

Project implication:
Inspect the available text, labels, duplicates, and source
distribution before selecting the dataset.

### 2.4 E-PhishGen

Pajola et al. (2025) examined phishing detection benchmarks
and introduced generated emails for additional evaluation.

The study reported lower performance on the new examples
than on existing benchmarks.

Relevance:
The study shows why strong results on one dataset may not
transfer to unfamiliar messages.

Limitation:
Generated emails do not fully represent real communication.

Project implication:
Include an independent evaluation source where possible
and report synthetic-data results separately.

### 2.5 Phishing, Spam, and Legitimate Email Classification

Toth et al. (2025) introduced a labelled email dataset
covering phishing, spam, and legitimate messages.
The study also examined emotional cues and rephrased emails.

Relevance:
This work supports distinguishing spam from phishing
and checking performance when wording changes.

Limitation:
Some annotations involve language models, and some examples
are generated or rephrased. Annotation quality and data
provenance require careful review.

Project implication:
Do not automatically treat spam as fraud. Keep related
original and rephrased examples in the same data split.

## 3. Speech Recognition Research

### 3.1 Whisper

Radford et al. (2022) introduced Whisper, a speech recognition
approach trained using large-scale multilingual supervision.

Relevance:
Whisper is a candidate for converting uploaded speech
recordings into text.

Limitation:
Speech recognition performance may vary across languages,
recording conditions, and speaking styles.
Whisper itself does not classify fraud.

Project implication:
Evaluate transcription quality and its effect on the
downstream fraud classifier.

### 3.2 Kazakh Speech Corpus 2

Mussakhojayeva et al. (2022) introduced KSC2, a large
Kazakh speech corpus with reference transcriptions.

Relevance:
KSC2 provides a resource for evaluating Kazakh speech
recognition.

Limitation:
It is a speech corpus, not a labelled fraud dataset.
It cannot independently evaluate fraud detection.

Project implication:
Use speech data to assess transcription quality.
Use separate labelled examples to assess the complete
speech-to-risk pipeline.

### 3.3 LoRA-Whisper

Song et al. (2024) investigated parameter-efficient
adaptation of Whisper for multilingual speech recognition.

Relevance:
This approach may be useful if the initial speech model
requires adaptation.

Limitation:
Adaptation still requires suitable recordings, reference
transcriptions, computing resources, and evaluation.

Project implication:
Start with an existing speech model. Consider adaptation
only if initial testing identifies a clear need.

## 4. Proposed Technical Direction

The initial text experiments will compare:

1. TF-IDF with Logistic Regression as the baseline.
2. Fine-tuned XLM-R as the modern approach.

Both approaches will use the same training, validation,
and test partitions for a fair comparison.

The planned speech approach is:

1. Convert an uploaded recording into text.
2. Pass the transcript to the text classifier.
3. Return the model's risk assessment.

These are preliminary choices, not completed experiments.

## 5. Evaluation Lessons

The reviewed work motivates the following evaluation plan:

- Measure Precision, Recall, F1, and ROC-AUC.
- Report results separately for each supported language.
- Prevent duplicate and related messages from crossing splits.
- Examine false positives and false negatives.
- Test unfamiliar message sources where possible.
- Measure speech recognition errors using Word Error Rate.
- Compare classification using reference and predicted transcripts.
- Evaluate score calibration before interpreting model scores
  as probabilities.

Published results from other studies will be used for context,
not presented as results achieved by our team.

## 6. Remaining Research Questions

- Which datasets adequately represent our selected fraud scenarios?
- Is sufficient labelled Russian and Kazakh text available?
- Does XLM-R improve performance over the baseline?
- How much do transcription errors affect fraud classification?
- How well do models trained on emails perform on short messages?
- Which errors are most harmful for the intended users?

## 7. References

1. Conneau et al. (2020).
   Unsupervised Cross-lingual Representation Learning at Scale.
   https://aclanthology.org/2020.acl-main.747/

2. Paul et al. (2024).
   Phishing Email Detection Using Inputs From Artificial Intelligence.
   https://arxiv.org/abs/2405.12494

3. Mendes et al. (2025).
   MeAJOR Corpus: A Multi-Source Dataset for Phishing Email Detection.
   https://arxiv.org/abs/2507.17978

4. Pajola et al. (2025).
   E-PhishGen: Unlocking Novel Research in Phishing Email Detection.
   https://arxiv.org/abs/2509.01791

5. Toth et al. (2025).
   Constructing and Benchmarking: a Labeled Email Dataset
   for Text-Based Phishing and Spam Detection Framework.
   https://arxiv.org/abs/2511.21448

6. Radford et al. (2022).
   Robust Speech Recognition via Large-Scale Weak Supervision.
   https://arxiv.org/abs/2212.04356

7. Mussakhojayeva et al. (2022).
   KSC2: An Industrial-Scale Open-Source Kazakh Speech Corpus.
   https://www.isca-archive.org/interspeech_2022/mussakhojayeva22_interspeech.html

8. Song et al. (2024).
   LoRA-Whisper: Parameter-Efficient and Extensible Multilingual ASR.
   https://arxiv.org/abs/2406.06619