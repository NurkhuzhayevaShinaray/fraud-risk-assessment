# 2. Evidence of Relevance

## 2.1. Purpose of User Research
The purpose of this research was to assess the practical relevance of the proposed Alay-Aq fraud-risk assessment web application and to identify user concerns that should inform its requirements. The research focused on experiences with suspicious text messages and calls, current verification practices, difficulties in recognizing fraudulent communications, preferred result explanations, privacy expectations, and interface accessibility.

The study provides exploratory evidence for requirements elicitation. It does not measure the accuracy of the proposed fraud-detection system, prove that fraud can be prevented, or establish that the application has already been implemented.

## 2.2. Research Methodology
Two complementary methods were used: (1) semi-structured written interviews with three potential users (P1-P3) and (2) a supplementary Google Forms questionnaire. The interviews used a ten-question guide designed to elicit detailed experiences and expectations. All three interviews contain responses to all ten questions. P3’s response to Question 6 is quoted in the evidence register.

The questionnaire explored exposure to suspicious communications, self-assessed confidence, current reactions, difficulties, potential use of text and audio analysis, preferred features, perceived importance of explanations, concerns about submitting material, and interface languages. The questionnaire dataset used for this analysis contains 13 responses with affirmative consent. Survey statistics are based on n = 13 consenting responses.

Interviewees are identified only as P1, P2, and P3. No participant names, usernames, exact interview dates, or contact details are reported. Survey results are presented only in aggregate. Multiple-choice questions allowed several selections; consequently, their counts may sum to more than 13. Interview and survey samples are not assumed to consist of 16 unique individuals because overlap cannot be verified.

## 2.3. Participants and Data Sources
**Table 2.1. Interview participants and available evidence**

| **ID** | **Relevant experience disclosed in the interview** | **Interview data available** |
| --- | --- | --- |
| P1 | Suspicious package-delivery and bank-verification messages, often including links and urgent requests. | Written responses to Q1-Q10 |
| P2 | A suspicious telephone call from a person claiming to represent a bank. | Written responses to Q1-Q10 |
| P3 | Prize/gift messages and calls from unknown numbers asking personal questions. | Written responses to Q1-Q10 |

All three interviewees described real or perceived encounters with suspicious communications. The source material does not establish their demographic profiles or recruitment categories beyond being potential users of digital communication services; therefore, ages, occupations, and places of residence are not reported.

## 2.4. Findings from the Three Interviews
The interview responses were reviewed thematically. The following findings refer to what these three participants reported, rather than to prevalence in the general population.

**Table 2.2. Interview findings and design implications**

| **Theme** | **Evidence from the interviews** | **Implication for Alay-Aq** |
| --- | --- | --- |
| Convincing impersonation and urgency | P1 described professional-looking delivery/bank messages; P2 described a convincing bank impersonation call; P3 mentioned formal language and official-looking logos. | Explain suspicious cues instead of relying on an unexplained risk label. |
| Verification through trusted channels | P1 checks official applications; P2 contacts the organization using its official number; P3 checks official sites and asks family. | Recommend independent verification using official websites, applications, or published contact information. |
| Explainable assessment | P1 requests highlighted suspicious phrases; P2 requests a short explanation and warning signs; P3 prefers Low/Medium/High with plain-language explanations. | Display risk level, indicators, explanations, and a clear non-guarantee disclaimer. |
| Actionable guidance | P1 asks what to do after clicking a link; P2 discusses exposure of bank details or money transfers; P3 requests simple step-by-step instructions. | Provide situation-specific recommendations, including official escalation channels where appropriate. |
| Privacy and low-friction access | P1 and P2 ask whether submitted content/audio is stored; all three prefer access without compulsory registration. | Minimize data retention, explain the handling of uploads, and avoid mandatory accounts for basic assessment if technically feasible. |
| Accessible interface and languages | P1 prefers straightforward navigation and Russian/English; P2 wants a professional interface; P3 wants a one-step paste-and-check workflow, simple buttons, larger text, and Kazakh. | Use clear layouts and language feasibility checks; do not promise unsupported languages. |

The interviews indicate a preference for a simple, direct text-analysis workflow, alongside qualified interest in audio analysis. P1 expected to use text checks more often, and P3 similarly preferred pasting a message, pressing a button, and receiving an understandable result. P3 considered audio upload useful but expected to use text checking more frequently. P2 saw potential value in reviewing recorded calls but raised explicit privacy concerns about audio uploads. These responses support making text checking the primary workflow while retaining audio as a proposed option subject to privacy safeguards and speech-processing feasibility.

No interviewee treated an automated risk label as sufficient proof of fraud. Across the answers, explanations, cautious communication of uncertainty, independent verification, and relevant next steps emerged as particularly important design considerations.

## 2.5. Supplementary Google Forms Findings
Of the 13 consenting respondents, 12 reported encountering suspicious messages or calls (seven “once or twice” and five “several times”); one reported no such experience. These results describe a small convenience sample and are not estimates of fraud prevalence.

**Table 2.3. Selected questionnaire results (n = 13)**

| **Measure** | **Responses** | **Interpretation for design** |
| --- | --- | --- |
| Reported suspicious messages/calls | 12/13 yes; 1/13 no | Relevant scenario among respondents; not population prevalence. |
| Selected communication channels | SMS 8; WhatsApp 8; regular calls 8; Telegram 2; social media 2 | Text and telephone contexts are relevant; channel selections were multiple-choice. |
| Difficulty: manipulation or urgency | 8/13 | Consider clearly explaining pressure and urgency cues. |
| Difficulty: assessing sender/caller trust | 6/13 | Recommend official independent verification. |
| Difficulty: legitimacy of a link or request | 4/13 | Explain link/request warning signs without claiming to verify all URLs. |
| Potential input: copied SMS/messenger text | 8/13 | Supports making pasted text a primary workflow. |
| Potential input: both text and audio | 5/13 | Supports considering both modalities, subject to privacy and feasibility. |
| Explanation-importance rating | 7/13 selected 4 or 5; 5 selected 3; 1 selected 1 (five-point response scale) | Explanations matter to several respondents; ratings vary. |
| Main concern: content privacy | 5/13 | Provide transparent retention and deletion information. |
| Main concern: understanding results | 4/13 | Use plain-language explanations and a clear presentation. |
| Main concern: inaccurate results | 2/13 | Show limitations and avoid certainty claims. |
| Main concern: trust in service | 2/13 | Make the application’s purpose and limitations transparent. |
| Preferred interface languages | Kazakh 11; Russian 8; English 1 | Prioritize feasibility assessment for Kazakh and Russian; multiple selections allowed. |

Among listed features, suspicious text checking was selected by eight respondents, risk-level display by five, uploaded-audio checking by three, explanation of suspicious content by three, and a simple interface by three. These are choices made in a multi-select item, not exclusive rankings. One open-text response suggested checking links and analyzing voice messages; another specifically requested a fraud-news section. Such suggestions can inform future scope discussions but are not evidence that automatic URL safety verification or a new AI service has been implemented.

The self-assessed ability to identify fraudulent messages had a median response of 3 on the questionnaire’s five-point scale. This should be treated as self-reported confidence, not an objective fraud-recognition test. The questionnaire also shows that blocking senders and ignoring or deleting suspicious communications were commonly selected reactions (11 and 9 respondents respectively, with multiple answers permitted).

## 2.6. Implications for the Requirements Specification
The evidence below connects observed user needs to already documented functional or non-functional requirements. The references indicate design relevance; they do not prove that the requirements are implemented or that the proposed system will achieve a particular detection accuracy.

**Table 2.4. Traceability from evidence to project requirements**

| **Evidence-based need** | **Evidence** | **Relevant requirement(s)** | **Design / acceptance implication** |
| --- | --- | --- | --- |
| Simple pasted-text assessment | P1 and P3; survey 8/13 selected copied SMS/messenger text | FR-01, FR-02 | Text input should be prominent, understandable, and validated. |
| Explained and non-definitive results | P1, P2, P3; survey 7/13 rated explanation 4–5 | FR-03, FR-04, FR-05, FR-32; NFR-09 | Show Low/Medium/High, suspicious indicators, concise explanation and disclaimer. |
| Situation-specific safety steps | P1, P2, P3 | FR-06, FR-20, FR-21 | Show concrete steps and official verification or assistance routes when appropriate. |
| Privacy for text and audio | P1, P2; survey privacy was top concern for 5/13 | FR-09, FR-25; NFR-04 | Disclose upload handling, delete temporary audio, avoid permanent storage of original submissions. |
| Optional audio workflow | P2; survey 5/13 selected both text and audio | FR-08, FR-10, FR-12 | Support appropriate audio formats only after speech-processing feasibility evaluation. |
| Accessible interface without mandatory registration | P1, P2, P3; survey 4/13 concerned about comprehension | NFR-08, FR-31; proposed UX condition | Use clear navigation and avoid account creation for basic checks if approved by the team. |
| Language accessibility | P1, P3; survey Kazakh 11, Russian 8, English 1 | FR-07; NFR-14 | Prioritize language feasibility testing; do not imply that preferred languages are already supported. |
| Fraud-awareness content | One survey free-text response; current project concept | FR-18, FR-22 | Keep educational materials and a proposed news section; automatic news collection remains optional (FR-23). |

The findings particularly reinforce explanation quality, privacy transparency, and actionable guidance. User preferences for Kazakh do not demonstrate that the planned NLP or speech-to-text models can process Kazakh reliably. Likewise, interest in suspicious-link checking should not be converted into a claim that the prototype actively visits or verifies URLs; that would require separate requirements and security evaluation.

## 2.7. Research Limitations and Supporting Evidence
The interview sample contains only three participants, and the questionnaire contains 13 consenting responses. Sampling was non-random, the demographic characteristics of respondents were not documented, and possible overlap between the two groups could not be established. All accounts are self-reported. The questionnaire allowed multiple selections and included one respondent who reported no suspicious encounters but still selected communication channels; channel counts should therefore be treated as selections rather than verified encounter histories. These limitations prevent statistically representative conclusions.

All three interview records contain responses to all ten interview questions, including P3’s response to Question 6. The questionnaire analysis includes only the 13 consenting responses. Neither method measures actual model performance, usability outcomes, the safety of submitted content, or the effectiveness of future recommendations.

The documentation includes Appendix A (interview question guide), Appendix B (anonymized interview evidence register), and Appendix C (supplementary questionnaire evidence). The findings-to-requirements traceability matrix is presented in Table 2.4 of the main section. Original interview messages, personal handles, and contact details are not included in this repository document.

Overall, the research supports the practical relevance of a cautiously presented fraud-risk assessment tool offering explainable results, straightforward navigation, privacy-preserving handling of submitted material, and actionable recommendations. These are preliminary user needs that guide the project specification and should be validated through subsequent prototype usability testing.

## Appendix A. Semi-Structured Interview Guide
Q1. Have you ever received a suspicious message or call?

Q2. What did you do?

Q3. What is the most difficult part of identifying fraud?

Q4. Which verification methods do you trust?

Q5. What information would help you?

Q6. What would you expect from the proposed website?

Q7. How should the results be presented?

Q8. What safety guidance would you expect?

Q9. What would make the application easy to use?

Q10. What feature is essential, and what might prevent you from using it?

## Appendix B. Interview Evidence Register
**Table B.1. Question coverage and anonymized evidence**

| **Question** | **P1** | **P2** | **P3** |
| --- | --- | --- | --- |
| Q1 - Suspicious contact | Parcel/bank verification texts | Bank-impersonation call | Prize/gift messages and unknown calls |
| Q2 - Response | Ignored links; checked official apps | Ended call; used official bank number | Ignored or consulted family |
| Q3 - Difficulty | Professional, formal messages | Convincing banking procedures | Official-looking logos; technical wording |
| Q4 - Trusted methods | Official websites/apps | Official contact details | Official websites and family advice |
| Q5 - Useful information | Specific suspicious message elements | Whether requests match legitimate practices | Plain explanation and next steps |
| Q6 - Website expectations | Quick pasted-text explanation; privacy | Text or recordings; audio privacy | Simple paste–click–result flow; audio potentially useful, but text likely used more often |
| Q7 - Results | Risk plus highlighted explanation | Short warning-sign list and disclaimer | Low/Medium/High, plain language, disclaimer |
| Q8 - Guidance | What to do after clicking a link | Actions after data disclosure or transfer | Simple urgent steps, who to contact |
| Q9 - Usability | Fast, simple, Russian/English; no account | Privacy information; no account | Large text, simple controls; Kazakh |
| Q10 - Essential / barrier | Explanations; no excessive personal data | Privacy; no guaranteed predictions | Practical advice; no complicated registration |

P3 - Q6 (verbatim, anonymized): “It should be simple and not confusing. Like, I paste a message, click a button, and get an answer. That would be really convenient! Uploading audio sounds useful too, but honestly, I would probably use the text checking feature more often.”

This register summarizes, rather than reproduces verbatim, the full responses from P1–P3. The original responses may be retained separately with restricted access for verification; they are not linked or embedded in this Markdown document.

## Appendix C. Supplementary Questionnaire Evidence
Source: Google Forms survey response export supplied by the project team. The analysis dataset contains 13 consenting participants (S01–S13); the denominator in every questionnaire statistic in Section 2 is n = 13. Counts are descriptive, and several questions permit multiple answers.

The supporting questionnaire dataset uses anonymous participant identifiers (S01–S13) and excludes email addresses and submission timestamps. The results in the main report are descriptive summaries of these 13 consenting responses.

The de-identified questionnaire responses (n = 13) are retained as a separate supplementary dataset. All aggregate findings relevant to this section are reported above.

The numeric results and their implications are reported in Table 2.3. The connections between verified findings and planned requirements are reported in Table 2.4. Those two tables form part of the main research report and are not duplicated in this appendix.
