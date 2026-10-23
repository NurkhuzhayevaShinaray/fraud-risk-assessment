# 3. Literature Review

## 3.1. Rule-Based and Blacklist Approaches

Rule-based systems identify suspicious communications through predefined indicators, such as known malicious links, suspicious phrases, or patterns associated with common fraud techniques. Blacklists can efficiently detect known malicious domains and previously identified threats.

However, their effectiveness depends on the quality and freshness of the rules and lists. A newly created malicious link or a message that uses unfamiliar wording may not match existing indicators. Rule-based systems can also generate false positives when legitimate messages contain urgent language or links.

Kavya and Sumathi review blacklist-based, similarity-based, machine-learning, deep-learning, graph-based, and ensemble approaches to phishing detection [1]. Their review highlights the importance of dataset diversity, robustness, and interpretability when developing systems for evolving attacks.

Rule-based detection can therefore serve as a baseline or a supplementary component, but it should not be treated as a complete solution.

## 3.2. Classical Machine Learning and Natural Language Processing

Classical machine learning methods classify text using features extracted from messages. Common techniques include Term Frequency - Inverse Document Frequency (TF-IDF), Naive Bayes, Logistic Regression, Support Vector Machines, and tree-based classifiers.

These methods are useful for a student project because they can provide an understandable baseline and often require fewer computational resources than large deep-learning models. They can learn associations between words, phrases, and fraud labels, but their performance depends on the dataset, preprocessing, and the similarity between training and real-world messages.

Al Saidat, Yerima, and Shaalan review NLP and machine-learning techniques for SMS spam and phishing detection [4]. Their work discusses the progression from rule-based methods to machine-learning and deep-learning approaches.

Boulieris et al. investigate fraud detection using natural language processing and introduce the FraudNLP dataset for online banking action sequences [2]. This work demonstrates the potential of NLP for fraud-related data, but its focus on banking actions means that its findings cannot automatically be transferred to ordinary suspicious messages or voice recordings.

Tun and Birks use NLP to analyze reports of scams from Singapore [6]. Their method uses similarity measures and TF-IDF to identify common terms and sequences of actions within scam narratives. This is useful for understanding recurring fraud patterns, but the analysis of reported incidents is different from detecting a new suspicious message before a user acts on it.

These studies support the use of text classification and linguistic indicators in the proposed application, while also showing the need to evaluate whether a method is suitable for the actual input type.

## 3.3. Deep Learning and Contextual Features

Deep-learning methods, including convolutional neural networks, recurrent neural networks, and embedding-based models, can learn more complex patterns than systems relying only on predefined keywords. Contextual representations may help identify suspicious meaning even when a message uses unfamiliar wording.

Nevertheless, high reported accuracy does not guarantee good performance in a new environment. A model may rely on accidental correlations in the training data, and its performance can decrease when scammers change their language or when users submit messages from a different language or communication channel.

Wilk-Jakubowski et al. systematically review machine-learning and neural-network approaches to phishing detection across 105 publications [8]. Their review discusses methodological issues such as dataset quality, data leakage, class imbalance, validation strategies, and the reporting of performance and system metrics.

Kavya and Sumathi also emphasize challenges related to adversarial robustness, dataset diversity, and explainability [1].

For the proposed project, these findings suggest that the selected analysis method should be evaluated on appropriate test data rather than chosen solely because a publication reports a high accuracy score.

## 3.4. Emotional and Phrase-Based Indicators

Fraudulent communications often rely on urgency, authority, fear, promises of financial gain, or pressure to take immediate action. These characteristics may provide useful signals in addition to individual keywords.

Krawczyk, Probierz, and Kozak investigate the use of emotion-based labels and phrase-level indicators in smishing detection [9]. Their experiments use more than 22,000 SMS messages. In one reported configuration, adding emotional and phrase-level features increased Logistic Regression accuracy with TF-IDF from 0.9186 to 0.9221. However, the authors also report that such features can reduce performance in some configurations.

This finding is important because it shows that an apparently meaningful feature does not necessarily improve a classifier. The usefulness of urgency, emotion, and suspicious phrases must be tested empirically.

The proposed application can use such indicators to explain why a message may be suspicious, but it should not classify a message as fraudulent solely because it contains emotional or urgent language.

## 3.5. Speech Processing and Voice Phishing Detection

Voice phishing presents additional challenges because spoken communication contains both linguistic content and acoustic information. A fraudulent call may involve impersonation, urgency, persuasive language, or a request for a financial action.

A practical audio-processing pipeline may include:

1. Accepting a supported audio recording.
2. Converting speech into text using a speech-to-text component.
3. Analyzing the resulting transcript for suspicious language and social engineering indicators.
4. Combining the available evidence into a risk assessment.
5. Presenting explanations and safety recommendations to the user.

Triantafyllopoulos et al. review the detection of social engineering in spoken communication and identify the need for more research on speech-based detection and effective user interventions [3]. The study is especially relevant because it treats vishing as a problem that involves communication and human behavior, rather than simply detecting particular words.

A recent open-access dataset study by Hmimou et al. introduces 3,000 simulated phone calls in English, French, and Modern Standard Arabic [10]. The data include annotations for persuasion strategies, interactional markers, and emotional tone. However, the recordings are synthetically generated, and the authors note that the acoustic conditions do not fully reproduce real telecommunication channels.

Hmimou et al. also present VISH-GUARD, a framework combining acoustic analysis, semantic intent, emotion detection, behavioral profiling, and large language model-based reasoning [11]. This provides an example of a more complex architecture for explainable vishing detection. However, the work is very recent and uses synthetic English, French, and Arabic data. Its results do not establish that the same system will perform reliably on Kazakh or Russian audio.

Kim's 2026 MVGC study analyzes Korean voice-phishing transcripts using text and structured representations of entities and relationships [12]. The paper reports that a text-only model performs strongly on its standard test split, while structural information becomes more useful under a stricter out-of-distribution evaluation. It also identifies transcript length as a possible shortcut in the standard benchmark.

These studies demonstrate that speech-based fraud detection is technically feasible, but they also reveal substantial challenges in dataset availability, language coverage, realistic audio conditions, and generalization. For this project, uploaded audio analysis with speech-to-text and transcript-based risk assessment is a more realistic initial scope than a complex multi-agent system or live-call monitoring.

## 3.6. Existing Applications and Dataset Quality

Akande et al. present SMSPROTECT, a mobile application that intercepts incoming SMS messages and sends them through an API to a rule-based detection model [7]. The study demonstrates how a detection method can be integrated into a user-facing application. However, its focus is SMS interception and classification, rather than a web application that accepts user-submitted text and audio recordings.

Johari et al. evaluate ten SMS spam datasets using Decision Tree and Multinomial Naive Bayes classifiers [5]. They consider dataset authenticity, class imbalance, feature diversity, metadata availability, and preprocessing requirements. Their findings show that dataset selection can influence both model performance and the difficulty of the detection task.

These results are relevant to the project's implementation and evaluation. A suitable model cannot be selected based only on its reported accuracy; the team must also consider the data used for training and testing, the supported language, the type of input, and the difference between spam detection and fraud detection.

## 3.7. Critical Synthesis and Research Gap

The reviewed literature establishes that fraud detection can use several complementary approaches:

- Rule-based indicators and blacklists for known threats and recognizable patterns.
- Classical machine learning for lightweight text classification.
- Deep learning and contextual representations for more complex language patterns.
- Emotion and phrase-level features for identifying possible social engineering cues.
- Speech-to-text processing and transcript analysis for uploaded audio recordings.
- More advanced acoustic, behavioral, or graph-based methods for specialized voice-phishing detection.

However, the literature also identifies several limitations.

First, many studies focus on a single input type, such as SMS, URLs, banking records, or call transcripts. Their findings are not necessarily transferable across these different domains.

Second, dataset quality and representativeness remain important concerns. A model trained on one language or dataset may not generalize to a different population, communication channel, or fraud technique.

Third, reported performance can be misleading if a dataset contains accidental correlations, duplicated examples, class imbalance, or an unsuitable evaluation split. Research should therefore report more than accuracy when the necessary data are available.

Fourth, speech-processing research increasingly uses complex architectures and synthetic datasets, but recent examples are not sufficient to establish reliable performance on Kazakh and Russian audio. This limitation must be addressed through language-specific feasibility checks and evaluation.

Finally, detecting suspicious content is only one part of the user problem. Users also need understandable explanations and recommendations. An application that returns a risk label without clarifying the suspicious indicators may provide limited practical value.

The research gap addressed by this project is the design and evaluation of an accessible user-facing application that combines text analysis and uploaded audio processing with understandable risk explanations and safety recommendations, while explicitly documenting language and dataset limitations.

The project does not claim to introduce a fundamentally new machine-learning algorithm. Its engineering contribution is the integration of suitable existing methods into a coherent application workflow, together with functional testing and a documented evaluation of its limitations.

## 3.8. Literature Review Matrix

To organize the reviewed literature according to the type of data and detection task, the selected studies were grouped into three thematic categories: general phishing detection approaches and evaluation, text-based fraud and SMS phishing detection, and voice phishing detection and speech analysis. This structure enables a comparison of established text-based methods with emerging speech-based approaches while identifying common methodological limitations and gaps relevant to the proposed system. The main characteristics, methods, findings, and limitations of the reviewed studies are summarized in Tables 1-3.

### Table 1. General Phishing Detection Approaches and Evaluation

| **No. / Source**                                                                                                 | **Study focus and data**                                                                                                          | **Method and comparison**                                                                                                                                       | **Main findings**                                                                                                                 | **Limitations and relevance**                                                                                                                                                           |
| ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [1] Kavya & Sumathi (2025). [Article](https://doi.org/10.1007/s10462-024-11055-z)         | Literature review of phishing-detection approaches. The exact number of reviewed studies is not available in the extracted notes. | Reviews blacklists, similarity-based methods, ML, DL, graph-based and ensemble approaches. No single head-to-head experiment is reported in the current notes.  | Highlights dataset diversity, robustness and interpretability as important concerns in phishing detection.                        | Detailed inclusion criteria and study count are unavailable. Supports method selection and systematic documentation of limitations.                                                     |
| [8] Wilk-Jakubowski et al. (2025). [Article](https://doi.org/10.3390/electronics14183744) | Systematic review of 105 publications on ML and neural-network approaches to phishing detection published between 2017 and 2024.  | Reviews detection approaches and evaluation practices across published studies. A single common experimental benchmark is not described in the extracted notes. | Identifies dataset quality, data leakage, class imbalance, validation and performance reporting as important evaluation concerns. | Findings depend on heterogeneous published studies, with no single pooled model comparison available in the extracted notes. Informs the evaluation methodology of the proposed system. |

### Table 2. Text-Based Fraud and SMS Phishing Detection

| **No. / Source**                                                                                           | **Study focus and data**                                                                                                                            | **Method and comparison**                                                                                                                                                  | **Main findings**                                                                                                           | **Limitations and relevance**                                                                                                                                                         |
| ---------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [2] Boulieris et al. (2024). [Article](https://doi.org/10.1007/s10994-023-06354-5)  | NLP-based fraud detection using online banking action sequences from the FraudNLP dataset. Exact sample size is unavailable in the extracted notes. | Applies NLP to fraud-related action sequences. Specific baselines and quantitative comparisons are unavailable in the extracted notes.                                     | Demonstrates the potential of NLP for identifying fraud-related patterns in textual action sequences.                       | Banking action sequences differ from ordinary messages and audio transcripts. Transfer to these input types is not established.                                                       |
| [4] Al Saidat et al. (2024). [Article](https://doi.org/10.1016/j.procs.2024.10.198) | Survey of NLP and ML techniques for SMS spam and phishing detection. The exact number of reviewed studies is unavailable.                           | Reviews rule-based, ML and DL approaches rather than testing one common benchmark, according to the extracted notes.                                                       | Describes the development of detection methods from rule-based systems to ML and DL approaches.                             | Dataset-level results and detailed review limitations are unavailable in the extracted notes. Supports the selection of candidate text-classification methods.                        |
| [5] Johari et al. (2025). [Article](https://doi.org/10.1038/s41598-025-92223-1)     | Empirical evaluation using ten SMS spam datasets.                                                                                                   | Evaluates Decision Tree and Multinomial Naive Bayes classifiers across datasets and examines dataset characteristics and preprocessing.                                    | Dataset authenticity, class imbalance, feature diversity, metadata and preprocessing affect detection results.              | Focuses on SMS data. Transferability to voice data and other languages is not established in the current review.                                                                      |
| [6] Tun & Birks (2023). [Article](https://doi.org/10.1186/s40163-022-00177-w)       | NLP analysis of reported scam narratives from Singapore. Exact sample size is unavailable in the extracted notes.                                   | Uses TF-IDF and similarity measures to identify recurring terms and sequences of scam actions. A specific baseline comparison is unavailable.                              | NLP can help identify recurring patterns in reported scam narratives.                                                       | Analysis of reported incidents differs from detecting new incoming messages. Supports the analysis of fraud patterns but does not directly establish real-time detection performance. |
| [7] Akande et al. (2023). [Article](https://doi.org/10.1016/j.icte.2022.05.009)     | Development of the SMSPROTECT mobile application for incoming SMS messages. Exact sample size is unavailable in the extracted notes.                | Integrates a rule-based detection model into a mobile application through an API that intercepts SMS messages. A direct comparison with alternative models is unavailable. | Demonstrates the integration of a detection method into a user-facing application.                                          | Focuses on SMS interception and does not establish performance for a web application accepting text and uploaded audio. Relevant to implementation and interface design.              |
| [9] Krawczyk et al. (2025). [Article](https://doi.org/10.1016/j.procs.2025.09.567)  | Experimental study of emotion- and phrase-based smishing detection using more than 22,000 SMS messages.                                             | Uses TF-IDF and Logistic Regression, comparing a baseline configuration with configurations incorporating emotional and phrase-level features.                             | Reported accuracy increased from 0.9186 to 0.9221 in one configuration. Performance decreased in some other configurations. | Benefits vary by configuration. Generalization to Kazakh and Russian messages is not established. Relevant to testing additional textual indicators empirically.                      |

### Table 3. Voice Phishing Detection and Speech Analysis

| **No. / Source**                                                                                                                                         | **Study focus and data**                                                                                                                                                           | **Method and comparison**                                                                                                                                                                                                                                                       | **Main findings**                                                                                                                                          | **Limitations and relevance**                                                                                                                                                             |
| -------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [3] Triantafyllopoulos et al. (2025). [Article](https://opus.bibliothek.uni-augsburg.de/opus4/frontdoor/index/index/docId/121734) | Survey and research roadmap covering vishing and spoken social engineering. The exact number of reviewed studies is unavailable in the extracted notes.                            | Reviews speech-based detection and related research challenges. No single controlled model comparison is reported in the current notes.                                                                                                                                         | Identifies vishing as a social-engineering problem and highlights the need for further research and effective user interventions.                          | Specific benchmarks and quantitative results are unavailable in the extracted notes. Provides the conceptual basis for audio-based fraud analysis.                                        |
| [10] Hmimou et al. (2026). [Article](https://doi.org/10.1038/s41597-026-07724-z)                                                  | Development of a multilingual speech dataset containing 3,000 simulated phone calls in English, French and Modern Standard Arabic.                                                 | Provides annotated speech data covering persuasion strategies, interactional markers and emotional tone. Direct classifier comparison is not applicable to its primary dataset-development contribution.                                                                        | Provides annotated multilingual speech data for research into vishing and social engineering.                                                              | Simulated calls may not fully reproduce real telecommunication conditions. Kazakh and Russian are not included. Highlights language coverage and audio realism as important requirements. |
| [11] Hmimou et al. (2026). [Article](https://doi.org/10.1038/s41598-026-71813-7)                                                  | Development of VISH-GUARD, a multi-agent framework for voice-phishing detection using synthetic multilingual speech data. Exact sample size is unavailable in the extracted notes. | Combines acoustic analysis, semantic intent, emotion detection, behavioral profiling and LLM-based reasoning. Specific baselines and comparative metrics are unavailable in the extracted notes.                                                                                | Presents a framework combining multiple evidence sources for voice-phishing detection.                                                                     | Uses synthetic multilingual data; reliable performance on Kazakh and Russian audio is not established. Provides a reference for future development beyond the initial project scope.      |
| [12] Kim (2026). [Article](https://doi.org/10.1016/j.icte.2026.07.013)                                                            | Experimental study of graph-based Korean voice-phishing detection using Korean voice-phishing transcripts. Exact sample size is unavailable in the extracted notes.                | Uses multi-view hyper-relational knowledge graph contrastive learning (MVGC), combining text with structured entity and relationship information. Compares text-only and structurally enriched approaches and examines standard versus stricter out-of-distribution evaluation. | Structural information becomes more useful under stricter out-of-distribution evaluation. Transcript length may act as a shortcut in a standard benchmark. | Focuses on Korean data, so transfer to Kazakh and Russian is not established. Transcript-length bias is an evaluation concern. Demonstrates the importance of testing generalization.     |


The reviewed studies demonstrate that phishing and fraud detection can be approached through rule-based methods, traditional machine learning, deep learning, natural language processing, and more advanced approaches involving speech analysis and structured knowledge. However, the effectiveness of these approaches depends on dataset quality, preprocessing, evaluation design, and the characteristics of the target input.

Text-based studies provide a foundation for identifying suspicious linguistic patterns and evaluating classification methods. Voice-phishing studies extend this direction by considering acoustic characteristics, emotional cues, spoken intent, and contextual information. Nevertheless, the reviewed research does not establish reliable performance for Kazakh and Russian text and audio inputs within a single integrated system. This limitation motivates further investigation into a system capable of analyzing text messages and uploaded audio while evaluating its performance on the intended language and data domains.

## References for the Literature Review
[1] S. Kavya and D. Sumathi, “Staying ahead of phishers: A review of recent advances and emerging methodologies in phishing detection,” *Artificial Intelligence Review*, vol. 58, art. no. 50, 2025. [ https://doi.org/10.1007/s10462-024-11055-z](https://doi.org/10.1007/s10462-024-11055-z)

[2] P. Boulieris et al., “Fraud detection with natural language processing,” *Machine Learning*, vol. 113, pp. 5087–5108, 2024. [ https://doi.org/10.1007/s10994-023-06354-5](https://doi.org/10.1007/s10994-023-06354-5)

[3] A. Triantafyllopoulos et al., “Vishing: Detecting social engineering in spoken communication—A first survey & urgent roadmap to address an emerging societal challenge,” *Computer Speech & Language*, vol. 94, art. no. 101802, 2025. [ https://doi.org/10.1016/j.csl.2025.101802](https://doi.org/10.1016/j.csl.2025.101802)

[4] M. R. Al Saidat, S. Y. Yerima, and K. Shaalan, “Advancements of SMS spam detection: A comprehensive survey of NLP and ML techniques,” *Procedia Computer Science*, vol. 244, pp. 248–259, 2024. [ https://doi.org/10.1016/j.procs.2024.10.198](https://doi.org/10.1016/j.procs.2024.10.198)

[5] M. F. Johari et al., “Key insights into recommended SMS spam detection datasets,” *Scientific Reports*, vol. 15, art. no. 8162, 2025. [ https://doi.org/10.1038/s41598-025-92223-1](https://doi.org/10.1038/s41598-025-92223-1)

[6] Z. L. Tun and D. Birks, “Supporting crime script analyses of scams with natural language processing,” *Crime Science*, vol. 12, art. no. 1, 2023. [ https://doi.org/10.1186/s40163-022-00177-w](https://doi.org/10.1186/s40163-022-00177-w)

[7] O. N. Akande et al., “SMSPROTECT: An automatic smishing detection mobile application,” *ICT Express*, vol. 9, no. 2, pp. 168–176, 2023. [ https://doi.org/10.1016/j.icte.2022.05.009](https://doi.org/10.1016/j.icte.2022.05.009)

[8] J. L. Wilk-Jakubowski, L. Pawlik, G. Wilk-Jakubowski, and A. Sikora, “Machine learning and neural networks for phishing detection: A systematic review (2017–2024),” *Electronics*, vol. 14, no. 18, art. no. 3744, 2025. [ https://doi.org/10.3390/electronics14183744](https://doi.org/10.3390/electronics14183744)

[9] N. Krawczyk, B. Probierz, and J. Kozak, “Emotion and phrase-based patterns in smishing: A feature-driven detection framework,” *Procedia Computer Science*, vol. 270, pp. 4421–4430, 2025. [ https://doi.org/10.1016/j.procs.2025.09.567](https://doi.org/10.1016/j.procs.2025.09.567)

[10] Y. Hmimou, M. Tabaa, A. Khiat, and Z. Hidila, “A multilingual behavioral speech dataset for vishing and social engineering detection,” *Scientific Data*, 2026. [ https://doi.org/10.1038/s41597-026-07724-z](https://doi.org/10.1038/s41597-026-07724-z)

[11] Y. Hmimou et al., “VISH-GUARD: A multi-agent and LLM-powered framework for multilingual voice phishing detection,” *Scientific Reports*, 2026. [ https://doi.org/10.1038/s41598-026-71813-7](https://doi.org/10.1038/s41598-026-71813-7)

[12] S. Kim, “MVGC: Multi-view hyper-relational knowledge graph contrastive learning for voice phishing detection,” *ICT Express*, 2026. [ https://doi.org/10.1016/j.icte.2026.07.013](https://doi.org/10.1016/j.icte.2026.07.013)

[13] General Prosecutor's Office of the Republic of Kazakhstan, “О криминогенной ситуации за 2024 год” [On the Crime Situation in 2024], Jan. 23, 2025. [Online]. Available: [ https://www.gov.kz/org/prokuror/press/article/details/192800?lang=ru](https://www.gov.kz/org/prokuror/press/article/details/192800?lang=ru)

[14] Government of the Republic of Kazakhstan, “«Закон и порядок» и защита цифровых прав граждан на уровне Конституции: в Казахстане число кибер-мошенничеств сократилось на 40%, потерпевшим возмещено 5,9 млрд теңге” [Law and Order and the Protection of Citizens' Digital Rights], Official Information Resource of the Prime Minister of the Republic of Kazakhstan, 2026. [Online]. Available: [ https://primeminister.kz/ru/news/reviews/zakon-i-poryadok-i-zashchita-cifrovyh-prav-grazhdan-na-urovne-konstitucii-v-kazahstane-chislo-kiber-moshennichestv-sokratilos-na-40-poterpevshim-vozmeshcheno-59-mlrd-tenge-31984](https://primeminister.kz/ru/news/reviews/zakon-i-poryadok-i-zashchita-cifrovyh-prav-grazhdan-na-urovne-konstitucii-v-kazahstane-chislo-kiber-moshennichestv-sokratilos-na-40-poterpevshim-vozmeshcheno-59-mlrd-tenge-31984)
