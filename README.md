# ScamAware MY — Document-Grounded Scam Awareness Assistant

> An AI assistant that answers questions about recognising online scams and what to do if affected, grounded in official Malaysian guidance and always showing its sources.

## Problem Statement
Online scams are widespread in Malaysia, and people need quick, trustworthy answers. Official guidance is spread across several agencies' web pages and changes over time, so users often rely on social media or general chatbots. A document-grounded assistant can retrieve the latest official guidance, answer in plain language and cite its sources.

## Evidence of the Problem
- Malaysia recorded 66,204 online scam cases in 2025, with losses of RM2.97 billion (New Straits Times, Jul 2026): https://www.nst.com.my/amp/news/nation/2026/07/1489207/rm38bil-wiped-out-online-scams-2025
- Guidance on the National Scam Response Centre (NSRC) differs across sources and has changed over time (reporting window and hotline hours): https://www.malaysia.gov.my/en/topics/nsrc-997-hotline and https://says.com/my/lifestyle/guide-what-to-do-if-scammed-in-malaysia

## Initial Related Work / Existing Approaches
- NSRC 997 hotline and Semak Mule portal — built for emergency reporting and checking, not for learning or follow-up questions.
- Bank Negara Malaysia fraud and scam notices — authoritative, but split across many separate notices.
- ScamPilot (Hoffman et al., 2026) — LLM-based scam training through simulation, not grounded in local official guidance. https://arxiv.org/abs/2601.22426v1
- General-purpose AI assistants — flexible, but not guaranteed to be grounded in current Malaysian procedures.

## Engineering Gap / Limitation
Official scam-prevention and response guidance in Malaysia is fragmented, changes over time, and is not available as a grounded, citable Q&A service. The assistant must answer from official documents, show the source and date, and refuse when the documents do not cover the question.

## Project Objectives
- O1: Design a document-grounded scam awareness assistant based on official Malaysian guidance.
- O2: Develop the assistant with retrieval, source citation, scope checks and a safety redirect for active loss or distress.
- O3: Evaluate answer correctness, groundedness, correct refusal and latency against a baseline using a test set of about 40 questions.

## Target Users
University students and young adults in Malaysia.

## Data Sources
- NSRC 997 Hotline (Malaysia.gov.my): https://www.malaysia.gov.my/en/topics/nsrc-997-hotline
- Bank Negara Malaysia, Fraud and Scam Notices: https://www.bnm.gov.my/fraud-and-scam-notices
- Bank Negara Malaysia, Scam Alerts: https://www.bnm.gov.my/scamalerts

Source URLs and access dates are kept in `data/`. Copyrighted or restricted documents are not committed to this repository.

## Out of Scope
Scam message detection, legal or financial advice, Malay-language support (possible future work), and storing user conversations.

## Weekly Progress
| Week | Focus | Deliverable | Status |
|------|-------|-------------|--------|
| W1 | System map + project scope | README + docs | ✅ |
