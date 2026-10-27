# Week 1 Project Scope

| Field | Content |
|---|---|
| **Project Name** | ScamAware MY — Document-Grounded Scam Awareness Assistant |
| **Domain** | Public safety / online fraud prevention |

## Problem Statement

Online scams are widespread in Malaysia, and people need quick, trustworthy answers about how to recognise common scams and what to do if they lose money. Official guidance is spread across several agencies' web pages and changes over time, so users often rely on social media or general chatbots. A document-grounded AI assistant can retrieve the latest official guidance, answer in plain language and cite its sources, which a simple keyword search over many separate pages cannot do well.

## Evidence of the Problem

- **Evidence 1:** Malaysia recorded 66,204 online scam cases in 2025, with losses of RM2.97 billion.
  Source: New Straits Times (Jul 2026), https://www.nst.com.my/amp/news/nation/2026/07/1489207/rm38bil-wiped-out-online-scams-2025
- **Evidence 2:** Guidance about the National Scam Response Centre (NSRC) is stated differently across sources and has changed over time. The official portal says to report within 24 hours and lists the 997 hotline as operating daily, 24 hours. An older guide refers to a 12-hour window. A news report from the centre's early period says 997 was reachable from 8 am. A 2026 article says the centre is now 24-hour and that calls to 997 are treated as police reports.
  Sources: https://www.malaysia.gov.my/en/topics/nsrc-997-hotline ; https://says.com/my/lifestyle/guide-what-to-do-if-scammed-in-malaysia ; https://soyacincau.com/?p=346789 ; https://says.com/my/tech/who-to-call-what-to-do-if-i-was-scammed-online-malaysia

## Initial Related Work / Existing Approaches

1. **NSRC 997 hotline and Semak Mule portal**
   Source: https://www.malaysia.gov.my/en/categories/safety-and-community/cybersecurity
   Key limitation: built for emergency reporting and checking account or phone details. It is not an interactive way to learn about scams or ask follow-up questions, and the hotline is not meant for follow-up enquiries.
2. **Bank Negara Malaysia fraud and scam notices**
   Source: https://www.bnm.gov.my/fraud-and-scam-notices
   Key limitation: authoritative, but split into many separate notices, so a user must search several pages to find the right advice.
3. **ScamPilot (Hoffman et al., 2026), an LLM-based conversational scam training tool**
   Source: https://arxiv.org/abs/2601.22426v1
   Key limitation: teaches users through simulated scam conversations. It does not answer questions from local official guidance, and it was not built for Malaysian procedures.
4. **General-purpose AI assistants** (for example ChatGPT or Claude)
   Key limitation: flexible, but not guaranteed to be grounded in current Malaysian official procedures, and may not cite sources.

## Engineering Gap / Limitation

Official scam-prevention and response guidance in Malaysia is fragmented across agencies, changes over time, and is not available as a grounded, citable question-and-answer service. The challenge is to answer accurately from official documents, show the source and date, and refuse when the documents do not cover the question.

## Initial Project Objectives

- **O1:** To design a document-grounded scam awareness assistant based on official Malaysian guidance.
- **O2:** To develop the assistant with retrieval, source citation, scope checks and a safety redirect for users who report an active loss or distress.
- **O3:** To evaluate answer correctness, groundedness, correct refusal of out-of-scope questions, and latency against a baseline using a test set of about 40 questions.

## Target Users

University students and young adults in Malaysia who want to learn how to recognise common scams and what to do if they are affected.

## Data Sources

- **Source 1:** NSRC 997 Hotline (Malaysia.gov.my) — https://www.malaysia.gov.my/en/topics/nsrc-997-hotline
- **Source 2:** Bank Negara Malaysia, Fraud and Scam Notices — https://www.bnm.gov.my/fraud-and-scam-notices
- **Source 3:** Bank Negara Malaysia, Scam Alerts — https://www.bnm.gov.my/scamalerts

## Similar to EduAdvisor

A document-grounded retrieval assistant that answers from official sources with citations, uses guardrails, and is evaluated on answer quality, groundedness, latency and safety.

## Different from EduAdvisor

- Different domain and users: public-safety guidance for the general public, instead of university advising.
- Sources are several agencies' web pages that change over time, so each source needs a date and version, and conflicting or outdated guidance must be handled.
- Time-critical advice: it must direct anyone reporting an active loss to the official hotline and the bank right away, instead of attempting to help.
- It is deliberately not a scam detector. It never says a specific message is safe or unsafe.

## Responsible AI Risks

- **Risk 1 — Outdated or incorrect procedure:** the assistant states an old reporting window or hotline hours, so a victim delays reporting and loses money.
- **Risk 2 — False reassurance:** a user asks whether a specific message or link is safe, and the system's answer makes them lower their guard. Mitigation: refuse to classify individual messages and explain the limits.
- **Risk 3 (privacy):** users paste bank details or personal information into the chat. Mitigation: warn users not to share them, avoid storing chat content, and avoid logging personal data.
- **Risk 4 (distress):** a user who has just been scammed is stressed or in distress. Mitigation: a guardrail that redirects to official channels (the 997 hotline, the bank and the police) and to appropriate support.

## Scope Boundaries

In scope: English-language Q&A from selected official documents. Out of scope for the semester: scam message detection, legal or financial advice, Malay-language support (possible future work), and storing user conversations.
