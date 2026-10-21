# Fraud Detection Scope

## 1. Purpose

The application will assess fraud risk in text messages and
uploaded speech recordings.

It will look for signs that a message attempts to obtain money,
passwords, verification codes, or other sensitive information
through deception.

The result will support the user's judgement. It will not prove
that a person or organisation is committing fraud.

## 2. Proposed Fraud Scenarios

The initial scope includes the following scenarios:

| Scenario | Description |
| --- | --- |
| Bank or support impersonation | A sender pretends to represent a bank or support service and requests sensitive information or a money transfer. |
| Fake delivery or payment request | A message asks the user to make a payment through a suspicious delivery or service request. |
| Fake prize or investment offer | A sender promises a reward or profit and requests an advance payment or personal information. |
| Friend or relative impersonation | A sender pretends to be a trusted person and urgently requests money. |

These scenarios are proposed research categories.
The final scope will depend on the availability and quality
of labelled datasets.

## 3. Initial Classification Task

The first version will use binary classification:

- Fraud-related: the message contains a deceptive request
  for money or sensitive information.
- Non-fraud-related: the message does not contain such a request
  according to the annotation guidelines.

Advertising and spam will not automatically be labelled as fraud.

Ordinary conversations, legitimate notifications, and
non-fraudulent advertising should be included as comparison examples.

Messages with insufficient context will be flagged for review
during annotation rather than assigned an unreliable label.

Predicting a separate fraud category is a possible later extension.
It is not a requirement for the initial classifier.

## 4. Input Types

The planned inputs are:

- Text entered or pasted by the user.
- An uploaded speech recording.

Speech will first be converted into text using a speech-to-text
model. The transcript will then be analysed by the text classifier.

The initial version will assess the content of speech.
It will not identify speakers or detect fraud from tone of voice.

## 5. Candidate Languages

English, Russian, and Kazakh are candidate languages.

English is proposed for initial experiments with public datasets.

Russian and Kazakh support will depend on the availability
of suitable labelled text data and the results of speech
recognition tests.

Performance must be evaluated separately for each supported language.
Mixed Russian–Kazakh speech will require a separate evaluation.

The final language scope will be agreed with the team and supervisor.

## 6. Planned Output

The application is expected to return:

- A Risk Score from 0 to 100.
- A Low, Medium, or High risk level.
- The transcript when the input is a speech recording.

The score calculation and risk thresholds will be defined
and validated during model evaluation.

The Risk Score will represent the model's assessment.
It will not be presented as a guaranteed probability of real fraud.

## 7. Out of Scope for the Initial Version

The initial version will not include:

- Live telephone call monitoring.
- Speaker identification or voice authentication.
- Deepfake voice detection.
- Image or video analysis.
- Website scanning or verification of a sender's identity.
- Automatic blocking of messages or financial transactions.

## 8. Decisions to Confirm

Before finalising the scope, the team must confirm:

- The main user group and its communication languages.
- Which fraud scenarios are covered by available datasets.
- The languages supported in the first version.
- Whether enough representative speech recordings are available
  for evaluation.