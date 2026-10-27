# Requirements Specification — ScamAware MY
## Section 0 — Project Framing & Application Scope Checkpoint

| Element | Content |
|---|---|
| **Problem Evidence** | **(1)** Malaysia recorded 66,204 online scam cases in 2025, with losses of RM2.97 billion (New Straits Times, Jul 2026: https://www.nst.com.my/amp/news/nation/2026/07/1489207/rm38bil-wiped-out-online-scams-2025). **(2)** Official guidance on reporting a scam is stated differently across sources and has changed over time (for example the reporting window and hotline hours for the National Scam Response Centre, NSRC): https://www.malaysia.gov.my/en/topics/nsrc-997-hotline compared with https://says.com/my/lifestyle/guide-what-to-do-if-scammed-in-malaysia. People therefore risk acting on outdated or inconsistent advice. |
| **Existing Approaches** | **1.** NSRC 997 hotline and Semak Mule portal — support urgent reporting and checking of account or phone details; not designed for learning or follow-up questions (https://www.malaysia.gov.my/en/categories/safety-and-community/cybersecurity). **2.** Bank Negara Malaysia fraud and scam notices and alerts — authoritative warnings about specific scam types; spread across many separate notices (https://www.bnm.gov.my/fraud-and-scam-notices ; https://www.bnm.gov.my/scamalerts). **3.** ScamPilot (Hoffman et al., 2026) — an LLM-based conversational tool that trains users to spot scams through simulation; not grounded in local official guidance (https://arxiv.org/abs/2601.22426v1). **4.** General-purpose AI assistants — flexible and conversational; not guaranteed to be grounded in current Malaysian procedures or to cite sources (to be tested as a baseline). |
| **Project / Engineering Gap** | Official scam-prevention and response guidance in Malaysia is fragmented across agencies, changes over time, and is not available as a grounded, citable question-and-answer service. The remaining limitation is practical: answering accurately from official documents, showing the source and its date, and declining when the documents do not cover the question. |
| **Objective O1** | To design a document-grounded scam awareness assistant based on official Malaysian guidance. |
| **Objective O2** | To develop the assistant with source citation, scope control, and a safety redirect for users who report an active loss or distress. |
| **Objective O3** | To evaluate answer correctness, groundedness, correct refusal and latency against a baseline, using a test set of at least 40 questions. |
| **Intended Users** | University students and young adults in Malaysia who want to learn how to recognise common scams and what to do if they are affected. |
| **Supported Tasks** | (a) Explain common scam types and their warning signs. (b) Explain the steps to take after a scam (for example contacting the bank, the NSRC hotline and the police) as stated in the sources. (c) Explain official ways to verify and report. (d) Show the source and date for every answer. |
| **Information / Knowledge Domain** | Official Malaysian online-fraud prevention and response guidance from approved public documents (initially the NSRC, Bank Negara Malaysia notices and scam alerts). English language. |
| **Operating Context** | A web chat used by students on a laptop or phone for non-emergency self-help. It is an information assistant and does not replace the bank, the NSRC or the police. |
| **Important Constraints** | Public documents only, with at least 3 sources; guidance changes over time, so each source needs a date and version; limited budget (free-tier or low-cost model access); one-semester timeline; no storage of user chat content or personal data; English only. |
| **Explicit Out-of-Scope Tasks** | Judging whether a specific message, link, phone number, account or offer is safe or fraudulent; legal, financial or investment advice; recovering money or predicting the outcome of a report; filing reports on the user's behalf; collecting personal or banking details; guidance from other countries. |
| **Evaluation Focus** | Does the assistant give correct, source-grounded and current guidance for in-scope questions, decline or redirect out-of-scope and active-loss situations appropriately, protect user privacy, and respond within an acceptable time, and does it do better than a baseline without access to the approved documents? |

### Objective-to-requirement check
| Objective | Supported by |
|---|---|
| O1 — design a document-grounded assistant | FR1, FR2, FR3, FR4, NFR4, RAI1, RAI5 |
| O2 — develop with citation, scope control and safety redirect | FR3, FR5, FR6, FR7, RAI2, RAI3, RAI4 |
| O3 — evaluate against a baseline | NFR1, NFR2, NFR3, NFR5, RAI1 – RAI5 |

---

## Section 1 — Functional Requirements

| # | Requirement — The system SHALL | Scope Boundary — SHALL NOT (where relevant) |
|---|---|---|
| **FR1** | Answer questions about common online scam types and their warning signs that are covered by the approved source documents. | Invent scam types, statistics or tactics that are not supported by the source documents. |
| **FR2** | Explain the steps a person should take after being scammed (for example contacting their bank, the NSRC hotline and the police) as stated in the approved sources. | Promise that money will be recovered or predict the outcome of a report. |
| **FR3** | Provide a source reference (document name and link) and the document's date for answers based on official documents. | Present unsupported information as if it came from an official source. |
| **FR4** | State clearly when the approved documents do not contain enough information to answer, and point the user to the relevant official channel. | Guess or answer from general knowledge as if it were official guidance. |
| **FR5** | Decline to judge whether a specific message, link, phone number, account or offer is safe or fraudulent, and instead explain general warning signs and how to verify through official channels. | Tell a user that a specific item is safe, or that it is definitely a scam. |
| **FR6** | When a user says they have already lost money or shared sensitive details, show the urgent official steps first, before any other information. | Delay the urgent steps or ask for personal or banking details. |
| **FR7** | Decline out-of-scope queries (for example legal, investment advice, non-Malaysian guidance or unrelated topics) and provide an appropriate redirect. | Provide legal, financial or investment advice. |

---

## Section 2 — Non-Functional Requirements

| # | Quality Attribute | Requirement | Measurement Method | Metric | Threshold |
|---|---|---|---|---|---|
| **NFR1** | Performance | The system shall keep interactive responses within an acceptable response time. | Measure end-to-end response time over the full evaluation question set. | p90 latency | < 5,000 ms |
| **NFR2** | Correctness | Answers shall be factually consistent with the approved source documents. | Score a curated set of at least 40 in-scope questions against a rubric (correct, partly correct, incorrect). | Correct response rate (%) | ≥ 80% |
| **NFR3** | Cost | Model usage cost shall stay within the project budget. | Record usage and cost over the evaluation workload. | Cost per 100 queries | < US$0.50 (illustrative) |
| **NFR4** | Maintainability / currency | A changed or newly added source document shall be reflected in answers without rebuilding unrelated components. | Run a controlled update test: change one source and confirm the answer changes. | Update time | < 10 minutes |
| **NFR5** | Reliability | The system shall return a usable response to valid requests without errors. | Run the evaluation workload and record failed or empty responses. | Error rate | ≤ 5% |

---

## Section 3 — Responsible AI Requirements

| # | Responsible AI Risk | Requirement | Measurement Method | Metric | Threshold |
|---|---|---|---|---|---|
| **RAI1** | Outdated or incorrect procedure | Procedural answers (reporting steps and hotline details) shall follow the latest approved source and show its date. | Test at least 10 procedural questions where older or conflicting sources exist and check against the latest approved source. | Procedural correctness rate; date shown rate | ≥ 95% correct; 100% date shown |
| **RAI2** | False reassurance | The system shall not classify a specific message, link, account or offer as safe or fraudulent. | Run a set of at least 20 "is this a scam?" queries about specific items. | Decline-and-redirect success rate; number of "safe" verdicts given | ≥ 95%; 0 |
| **RAI3** | Privacy | The system shall warn users not to enter personal or banking details, shall not store chat content, and shall mask personal identifiers before text is sent to any external model service. | Run at least 10 test cases with fake personal identifiers; inspect stored logs and outgoing requests. | Number of personal identifiers stored or transmitted unmasked | 0 |
| **RAI4** | Distress / active loss | When a user indicates an active loss or distress, the system shall show the urgent official steps and direct the user to appropriate human support. | Run a set of at least 10 test messages that describe an active loss or distress. | Urgent redirect success rate | ≥ 95% |
| **RAI5** | Transparency / grounding | The system shall provide a verifiable source reference for answers based on documents and say when it cannot find enough supporting evidence. | Review document-grounded answers for citation presence and check whether each cited source supports the answer. | Citation presence rate; citation-source match rate | 100% presence; ≥ 95% match |
