# 1. Project Proposal

## 1.1. Project Title

Development of an Application for Fraud Risk Assessment Based on Text and Speech Data Analysis

**Project name:** Alay-Aq

## 1.2. Team Members

Team members:

- Kissami Shakhnaz - ML/NLP and Speech Analysis: Responsible for researching and implementing methods for detecting potential fraud in text and speech data, selecting suitable datasets, and evaluating model performance.
- Nurkhuzhayeva Shinaray - Backend and System Architecture: Responsible for backend development, API design, data processing, and integration of the analysis models with the application.
- Botabaeva Saltanat - Frontend, Analytics, QA and Documentation: Responsible for user interface development, user requirements analysis, testing, quality assurance, and project documentation.

## 1.3. Supervisor

Supervisor: Serek Azamat Galymzhanovich

## 1.4. Problem Statement

Fraudulent communications are a significant cybersecurity concern because scammers use phishing messages, impersonation, false investment offers, urgent requests, and other social engineering techniques to persuade people to disclose sensitive information or transfer money. Such communications may imitate banks, government institutions, delivery services, and other trusted organizations.

The problem is relevant to Kazakhstan. According to the Prosecutor General's Office of the Republic of Kazakhstan, 45,156 fraud offences were registered in 2024, including 22,870 internet-fraud cases. The latter figure represented a reported increase of approximately 5% compared with 2023 [13]. A subsequent government publication reported 27,892 registered internet-fraud cases for the full year 2025 and 14,414 cases recorded during the reported part of 2026 [14]. Because the 2026 figure covers only part of the year, and the reports may use different reporting periods or definitions, these figures should not be treated as a directly comparable annual time series.

These statistics demonstrate the public relevance of fraud prevention. However, they do not independently establish the needs of the application's intended users or prove that the proposed solution will reduce fraud-related losses. User requirements must therefore be informed by exploratory discussions and evaluated through prototype testing.

People who receive suspicious messages or recordings may need support in recognizing warning signs, understanding potential risks, and identifying appropriate next steps. Existing solutions offer different forms of protection, including message filtering, suspicious-link analysis, caller screening, and fraud-prevention information. Their capabilities and limitations will be examined through a separate existing-system comparison rather than assumed without evidence.

The Alay-Aq project proposes a web application for assessing the potential fraud risk of user-submitted text and prerecorded audio. Supported audio recordings will be transcribed before their textual content is analyzed. The application is intended to present an indicative risk assessment, relevant warning indicators where technically supported, and practical safety recommendations.

Alay-Aq will function as a decision-support tool. It will not identify perpetrators, verify caller identities, guarantee the detection of fraud, or certify that a message assessed as low risk is safe.

## 1.5. Target Users

The primary intended users of Alay-Aq are individuals in Kazakhstan who wish to examine suspicious text messages or prerecorded spoken communications and obtain understandable fraud-risk information.

Potential user groups include:

- General users of messaging, telephone, and online communication services.
- Students and young adults interested in fraud awareness and online safety.
- People who prefer clear explanations and step-by-step instructions rather than technical security terminology.
- Users of digital banking and online services who want additional guidance when assessing suspicious communications.

These groups remain preliminary design assumptions. Three exploratory user interviews and a supplementary questionnaire have provided initial feedback on user needs, but their small samples do not establish that every assumed user group is representative. Further usability evaluation will be needed.

Kazakh and Russian are relevant potential languages for the intended audience. However, the application's initial supported languages will be determined by the availability of suitable datasets, speech-to-text functionality, and language-specific evaluation results. Unsupported languages will not be presented as validated.

## 1.6. Project Aim

The aim of this project is to develop and evaluate a web application that assesses potential fraud risk through text and uploaded audio data analysis, identifies suspicious indicators, explains the assessment results, and provides practical recommendations to help users respond safely to potentially fraudulent communications.

## 1.7. Project Objectives

The project has the following objectives:

1. Review recent scientific literature on phishing, smishing, vishing, natural language processing, speech processing, and fraud risk assessment.
2. Analyze existing fraud detection systems and identify their capabilities, limitations, and opportunities for improvement.
3. Define the target users, functional requirements, non-functional requirements, and privacy considerations.
4. Design the application architecture, user interface, and communication between the frontend, backend, and analysis components.
5. Develop a web interface for submitting text and uploading supported audio recordings.
6. Integrate suitable text classification and speech-processing methods, including speech-to-text transcription where required.
7. Develop a results interface that presents the estimated risk level, suspicious indicators, explanations, and safety recommendations.
8. Develop educational content about common fraud techniques and a Safety Assistant for responding to suspicious situations.
9. Test the application's functionality, integration, usability, and analysis performance using appropriate evaluation metrics.
10. Document the implementation, evaluation results, limitations, and possible future improvements.

## 1.8. Expected Outcomes

The expected outcome is a functional prototype of a fraud risk assessment application with the following features:

- Home: Displays relevant fraud alerts, news, and safety information.
- Fraud Checker: Accepts text input and supports uploaded audio recordings for analysis.
- Results and Recommendations: Presents the estimated fraud risk, suspicious indicators, explanations, and recommended actions.
- Learn: Provides educational information about common fraud techniques and prevention.
- Safety Assistant: Provides practical guidance for users who encounter suspicious communications or suspect that they have been targeted by fraud.

The project is expected to produce a working application prototype, an integrated text and speech analysis workflow, documented system architecture, test results, and project documentation.

The application will provide an indicative risk assessment rather than guarantee that a communication is fraudulent or legitimate. Its reliability will depend on the selected models, available datasets, supported languages, and evaluation results.

## 1.9. Project Scope

### Preliminary Project Scope

**Included in Scope**

The proposed project includes:

- Text submission and analysis.
- Uploading supported audio recordings for analysis.
- Speech-to-text transcription when necessary for audio analysis.
- Detection of suspicious linguistic patterns and potential social engineering indicators.
- Estimation and presentation of fraud risk.
- Explanations of suspicious indicators and practical safety recommendations.
- Educational materials about fraud prevention.
- A Safety Assistant for common suspicious situations.
- Frontend and backend development and integration.
- Testing, evaluation, and technical documentation.

The planned application will consist of five main pages: Home, Fraud Checker, Results and Recommendations, Learn, and Safety Assistant.

The initial implementation is expected to use existing models, libraries, and datasets where appropriate. Support for Kazakh and Russian will be considered according to the availability of suitable resources and the results of language-specific testing.

The exact implementation approach for the Safety Assistant, the final ML models, supported languages, and technical limitations have not yet been fully agreed upon by the team. These decisions will be refined during technical feasibility assessment and discussions with the supervisor.

**Excluded from Scope**

The following features are not currently planned for the initial project scope:

- Video files, video analysis, and video-call analysis.
- Live phone-call monitoring or interception.
- Automatic blocking of calls, messages, or financial transactions.
- Direct integration with bank accounts or access to confidential banking information.
- Guaranteed detection of every fraud attempt.
- A production-scale commercial security platform.

These preliminary boundaries help the team focus on developing and evaluating a feasible prototype. The scope may be refined following team discussions, technical evaluation, and supervisor feedback.

## 1.10. Project Feasibility and Engineering Complexity

### Clarity of the Problem

The project addresses a specific user problem: people may receive suspicious text messages or audio communications but lack an accessible way to assess potential fraud risk and understand what to do next.

The proposed solution has a clearly defined input, processing workflow, and output. Users submit text or an audio recording; the system processes the input using suitable analysis methods; and the interface presents an estimated risk level, suspicious indicators, and recommendations.

The system is intended to provide decision support, not to replace official verification or guarantee fraud detection.

### Realism of the Project Scope

The scope is realistic because it focuses on two input types: text and uploaded audio recordings. The project does not require real-time call interception, video analysis, financial transaction integration, or the development of a new large-scale machine learning model from scratch.

The team can use existing models and open-source tools, subject to licensing, language support, and technical feasibility checks. The final supported audio formats and languages will be determined during implementation and testing.

If reliable processing is not available for a particular language or audio format, this limitation will be documented rather than presenting unsupported functionality as completed.

### Engineering Complexity

The project involves sufficient engineering complexity for a software engineering diploma because it combines several interconnected components:

- Frontend engineering: Designing a usable interface for text input, audio uploads, results, education, and safety guidance.
- Backend engineering: Implementing API endpoints, input validation, file handling, error handling, and communication with analysis components.
- Text processing: Applying NLP methods to identify linguistic patterns associated with phishing and social engineering.
- Speech processing: Processing supported audio recordings and using speech-to-text transcription where required.
- System integration: Connecting the user interface, backend, transcription component, risk assessment method, and results presentation.
- Quality assurance: Testing normal and invalid inputs, processing failures, output consistency, and usability.
- Evaluation: Measuring classification performance where labelled data are available and documenting false positives, false negatives, and language limitations.
- Privacy and security: Minimizing unnecessary data collection, validating uploaded files, and avoiding the storage of sensitive user information when it is not required.

The engineering contribution is therefore not limited to creating a user interface. It involves designing, implementing, integrating, and evaluating a complete application workflow.

## 1.11. Connection Between the Project Proposal and Literature Review

The Literature Review provides the scientific basis for the proposed application. Recent studies examine phishing detection using rule-based methods, classical machine learning, deep learning, natural language processing, and speech analysis [1]–[12].

Research on SMS fraud demonstrates that text classification and linguistic indicators can support detection, while research on vishing highlights the challenges of analyzing spoken social engineering [3], [4], [7], [9]. Dataset studies also show that the selection, quality, balance, and representativeness of training data affect the reliability of evaluation [5], [8], [10].

These findings inform the project's design decisions. The application will focus on text and uploaded audio recordings, use existing methods where feasible, explain the detected suspicious indicators, and provide practical recommendations. It will not claim universal detection accuracy or assume that results obtained from English, Korean, French, or Arabic datasets automatically apply to Kazakh and Russian.

The Literature Review therefore supports the problem definition, technical approach, project boundaries, and evaluation strategy.

## References cited in this section

The full list of research publications [1]–[12] will be maintained in `literature-review.md`. The following official publications support the Kazakhstan statistics cited in Section 1.4:

[13] General Prosecutor's Office of the Republic of Kazakhstan, “О криминогенной ситуации за 2024 год” [On the Crime Situation in 2024], Jan. 23, 2025. https://www.gov.kz/org/prokuror/press/article/details/192800?lang=ru

[14] Government of the Republic of Kazakhstan, “«Закон и порядок» и защита цифровых прав граждан на уровне Конституции: в Казахстане число кибер-мошенничеств сократилось на 40%, потерпевшим возмещено 5,9 млрд теңге,” Official Information Resource of the Prime Minister of Kazakhstan, 2026. https://primeminister.kz/ru/news/reviews/zakon-i-poryadok-i-zashchita-cifrovyh-prav-grazhdan-na-urovne-konstitucii-v-kazahstane-chislo-kiber-moshennichestv-sokratilos-na-40-poterpevshim-vozmeshcheno-59-mlrd-tenge-31984
