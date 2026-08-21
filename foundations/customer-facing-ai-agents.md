---
type: Reference
title: Customer-Facing AI Agents
description: What a machine speaking for your brand must disclose, what escalation the messaging platforms actually require and what the brand is bound by when the model gets it wrong.
tags: [ai-agents, conversational, disclosure, consent, compliance, escalation, liability]
generated:
  by: human:jacquescorbytuech
  at: 2026-08-21T00:00:00Z
stale_after: 2027-02-21
sources:
  - id: whatsapp-business-messaging-policy
    resource: https://whatsappbusiness.com/policy/
    title: "Meta, WhatsApp Business Messaging Policy (automation and escalation paths)"
  - id: meta-whatsapp-cloud-api-send-messages
    resource: https://developers.facebook.com/docs/whatsapp/cloud-api/guides/send-messages/
    title: "Meta, WhatsApp Cloud API, sending messages and the customer-service window"
  - id: apple-messages-conversation-best-practices
    resource: https://register.apple.com/resources/messages/messaging-documentation/conversation-best-practices
    title: "Apple, Messages for Business conversation best practices (automated disclosure, auto-welcome)"
  - id: apple-messages-policies
    resource: https://register.apple.com/resources/messages/messaging-documentation/policies
    title: "Apple, Messages for Business policies (no bot-only solution, live agent access)"
  - id: apple-messages-faq
    resource: https://register.apple.com/resources/messages/messaging-documentation/faq
    title: "Apple, Messages for Business FAQ (mandatory escalation path)"
  - id: google-rbm-agents
    resource: https://developers.google.com/business-communications/rcs-business-messaging/guides/build/agents
    title: "Google, RCS Business Messaging agents (definition of an agent)"
  - id: google-rbm-best-practices
    resource: https://developers.google.com/business-communications/rcs-business-messaging/guides/learn/best-practices
    title: "Google, RCS Business Messaging best practices (chatbot persona guidance)"
  - id: eu-ai-act-2024-1689
    resource: https://eur-lex.europa.eu/eli/reg/2024/1689/oj/eng
    title: "Regulation (EU) 2024/1689, the AI Act (Article 50 transparency obligations)"
  - id: eu-regulation-2026-1744
    resource: https://eur-lex.europa.eu/eli/reg/2026/1744/oj/eng
    title: "Regulation (EU) 2026/1744 amending the AI Act"
  - id: california-bpc-17941
    resource: https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?lawCode=BPC&sectionNum=17941
    title: "California Business and Professions Code section 17941 (B.O.T. Act)"
  - id: ecfr-16-cfr-461
    resource: https://www.ecfr.gov/current/title-16/chapter-I/subchapter-D/part-461
    title: "16 CFR Part 461, FTC rule on impersonation of government and businesses"
  - id: fcc-declaratory-ruling-24-17
    resource: https://docs.fcc.gov/public/attachments/FCC-24-17A1.pdf
    title: "FCC, Declaratory Ruling FCC 24-17, CG Docket No. 23-362 (AI-generated voices under the TCPA)"
  - id: ecfr-47-cfr-64-1200
    resource: https://www.ecfr.gov/current/title-47/section-64.1200
    title: "47 CFR 64.1200, delivery restrictions on telephone calls and texts"
  - id: cbc-air-canada-chatbot
    resource: https://www.cbc.ca/news/canada/british-columbia/air-canada-chatbot-lawsuit-1.7116416
    title: "CBC, Air Canada ordered to honour discount its chatbot invented"
  - id: mccarthy-moffatt-v-air-canada
    resource: https://www.mccarthy.ca/en/insights/blogs/techlex/moffatt-v-air-canada-misrepresentation-ai-chatbot
    title: "McCarthy Tétrault, Moffatt v Air Canada, misrepresentation by an AI chatbot"
  - id: arstechnica-cursor-support-bot
    resource: https://arstechnica.com/ai/2025/04/cursor-ai-support-bot-invents-fake-policy-and-triggers-user-uproar/
    title: "Ars Technica, Cursor AI support bot invents fake policy and triggers user uproar"
  - id: bbc-dpd-chatbot
    resource: https://www.bbc.co.uk/news/technology-68025677
    title: "BBC News, DPD error caused chatbot to swear at customer"
  - id: markup-nyc-chatbot
    resource: https://themarkup.org/news/2024/03/29/nycs-ai-chatbot-tells-businesses-to-break-the-law
    title: "The Markup, NYC's AI chatbot tells businesses to break the law"
  - id: owasp-llm01-prompt-injection
    resource: https://genai.owasp.org/llmrisk/llm01-prompt-injection/
    title: "OWASP, LLM01 prompt injection"
  - id: nist-ai-100-2-e2025
    resource: https://csrc.nist.gov/pubs/ai/100/2/e2025/final
    title: "NIST AI 100-2 E2025, adversarial machine learning taxonomy and terminology"
---

## What it is

A customer-facing AI agent is a model composing the brand's half of a conversation with a customer: a WhatsApp support thread, an in-app chat window, an RCS reply, an email response. Two sets of rules govern it and they point at different things. Messaging platforms mostly regulate whether a human is reachable; disclosure duties come from statute, narrower and more jurisdiction-bound than the general advice suggests. The exposure that has actually cost companies money is neither of those: it is being held to what the agent said.

Agents that operate the marketing stack rather than talk to customers, holding credentials and firing sends and editing suppression, are a separate surface with its own threat model; see [AI agents and platform access](/foundations/ai-agents-and-platform-access.md). Voice is separate again, because in the US the consent rules turn explicitly on synthetic speech; see [voice](/channels/voice.md).

## What the platforms require

Meta's WhatsApp Business Messaging Policy allows automation during the 24-hour window but requires escalation paths that are prompt, clear and direct alongside it: in-chat transfer to a human agent, a phone number, an email address, web support, an in-store visit or a support form. Nothing in the policy requires you to tell a customer they are talking to a machine. Its body has no occurrence of artificial intelligence, AI agent, chatbot or any form of the word disclose. The nearest adjacent duty, anti-impersonation, governs business identity rather than human-versus-machine identity. Any disclosure duty on WhatsApp is imported from law; what Meta enforces is a reachable human. The window mechanics in [conversational messaging](/channels/conversational-messaging.md) are indifferent to who composes the reply.

Apple Messages for Business sets the ceiling. A bot must immediately disclose that it is automated and send an auto-welcome within five seconds of the first message; every agent, live or automated, should self-identify on its first reply. Apple's policies go further than any other platform on escalation: a business must not provide a limited or bot-only solution and must give access to a live agent during its regular business hours. Its FAQ makes a clear escalation path mandatory and states that deployments without live agent support will not be approved. The keyword to reach a person is `agent`, with `support` and `help` as alternatives. Apple also directs that customers be told when they are transferred and that the live agent introduce themselves.

RCS carries a terminology collision. In RCS Business Messaging an agent is the brand's registered sender identity, which Google defines as a programmatic entity sending messages on behalf of a brand, including any interface users interact with plus the code powering it. A brand can run an RBM agent with nothing but scripted templates behind it; an AI system can equally drive one. Google's agent documentation makes no mention of AI, chatbots or automated conversation. Verification there establishes the brand's right to manage the sender rather than anything about an AI system. Bot disclosure appears in RCS only as best-practice guidance, advising that a persona such as a virtual assistant or digital concierge be clearly identified as a chatbot. The Acceptable Use Policy carries no such requirement. See [SMS and RCS](/channels/sms-and-rcs.md).

## What the law requires

In the EU, Article 50(1) of the AI Act requires systems intended to interact directly with natural persons to be built so those persons are informed they are interacting with an AI system, unless that is obvious to a reasonably well-informed, observant and circumspect person. Article 50(5) fixes the timing at the first interaction or exposure. Article 50 sits in Chapter IV, applying from 2 August 2026. The obligation falls on the system's provider rather than the deploying brand, though a brand building its own agent occupies both roles. Regulation (EU) 2026/1744, in force from 27 July 2026, amended the AI Act without touching Chapter IV or moving that date.

In California, the B.O.T. Act makes it unlawful to use a bot to communicate with a person in California online with intent to mislead them about its artificial identity, in order to deceive them about the content of the communication and incentivise a purchase or sale. Disclosure that it is a bot removes liability; it must be clear, conspicuous and reasonably designed to inform. The scope limit matters as much as the prohibition: the statute keys to "online", defined as any public-facing website, web application or digital application. Whether that reaches a one-to-one SMS or WhatsApp thread is unsettled, with no case law or Attorney General opinion on the point. The 2026 companion-chatbot statute there expressly excludes bots used only for customer service or a business's operational purposes, which puts a CRM agent outside it.

In the US federally, no FTC rule requires an AI chatbot to disclose that it is not human. `16 CFR Part 461` covers impersonation of government and of businesses only; the proposed extension to impersonation of individuals was never finalised. Enforcement rests on general Section 5 deception and unfairness authority, applied case by case. See [legislation and compliance](/references/legislation-and-compliance.md).

## Voice and text are not symmetric

> [!warning] The AI-voice rule does not generalise to AI-written text
> The FCC's February 2024 ruling reached AI-generated voices under the TCPA's restriction on artificial or prerecorded voice. Its holding is confined to voice. An August 2024 FCC proposal on AI disclosure for autodialled texts noted expressly that the proposed on-call disclosure would apply only to voice calls and not to text messages. Nothing has been adopted since.

In the US, `47 CFR 64.1200` as of 1 August 2026 contains no occurrence of artificial intelligence or AI-generated. Consent rules there turn on the sending equipment and the channel rather than on whether a human or a model composed the words. Generalising the AI-voice ruling to AI-written SMS gets the analysis wrong in both directions. Consent capture across channels is in [consent and preferences](/foundations/consent-and-preferences.md).

## What the brand is bound by

> [!danger] The company owns what its bot says
> In *Moffatt v Air Canada*, the airline argued its chatbot was "a separate legal entity that is responsible for its own actions". The tribunal called the submission remarkable and held that a chatbot is still part of the company's website: it makes no difference whether the information comes from a static page or a chatbot.

Air Canada's chatbot told a customer he could book at full price and claim bereavement rates retroactively, which was untrue. The tribunal held that the applicable standard of care requires a company to take reasonable care that its representations are accurate and not misleading; Air Canada had not met it. Damages and fees came to CAD 812.02.

The weight of that decision needs stating honestly: the Civil Resolution Tribunal is British Columbia's online small-claims body, which makes this a first-instance decision in one province on a claim worth roughly CAD 800. It binds nobody in the UK, EU or US and sets no precedent there. What it defensibly shows is a company arguing its chatbot was a separate legal person and losing, with the tribunal treating chatbot output as no different from any other statement the company published.

The same line runs through the documented failures. In April 2025 a support bot for the code editor Cursor, replying as "Sam", told users the product was designed to work with one device per subscription as a core security feature. No such policy existed. Users read the reply as official and publicly cancelled subscriptions; the company confirmed it had no such policy, called the reply an incorrect response from a front-line AI support bot and now labels AI responses used for email support. In January 2024 a customer prompted the delivery company DPD's chat agent into swearing and into writing a poem calling DPD the worst delivery firm in the world; DPD blamed an error after a system update and disabled the AI element. In March 2024 New York City's business chatbot told employers they could take a cut of workers' tips and told landlords they need not accept housing vouchers, both contrary to local law. These are three shapes of one problem: an unconstrained generator speaking with the institution's authority.

## Prompt injection reaches this surface too

On a conversational channel the untrusted input is the inbound customer message itself, which leaves no perimeter at which to filter it out. OWASP treats indirect prompt injection as arising whenever a model accepts input from external sources and says it is unclear whether fool-proof prevention exists, given the stochastic behaviour at the heart of how models work. NIST explains that generative models combine the data and instruction channels, letting an attacker use the data channel to affect system operations. Its conclusion is that designers should assume prompt injection is possible wherever a model meets untrusted input. The depth treatment lives in [AI agents and platform access](/foundations/ai-agents-and-platform-access.md).

## Before you put one in front of customers

* **Fix the disclosure line once and apply it everywhere.** Apple already requires immediate self-identification; the EU AI Act requires it from 2 August 2026; the California statute makes it a liability shield. One global line costs less than per-jurisdiction variants and arguments about which thread counts as "online".
* **Guarantee a reachable human and test the path.** Walk it as a customer would: type `agent`, ask for a person in an unusual phrasing, try it outside business hours and confirm what actually happens.
* **Constrain what the agent may assert.** Policy, price, entitlement, eligibility and refunds are where an invented answer becomes a representation the brand is answerable for. Serve those from retrieved source text or fixed templates rather than free generation; the discipline on claims and wording sits in [copywriting](/foundations/copywriting.md).
* **Log every conversation with the model version and the retrieved context.** A complaint about what the bot said is unanswerable without the transcript.
* **Decide in advance what the agent must refuse.** Legal advice, medical or financial guidance, anything touching a live dispute and anything outside the retrievable knowledge base should hand off. An agent with no explicit refusal set will guess.
* **Keep the service thread separate from the promotional one.** An agent that starts selling inside a support conversation changes the message's class and the consent that governs it; see [transactional messaging](/foundations/transactional-messaging.md).

## Related

* [AI agents and platform access](/foundations/ai-agents-and-platform-access.md)
* [Voice](/channels/voice.md)
* [Conversational messaging](/channels/conversational-messaging.md)
* [SMS and RCS](/channels/sms-and-rcs.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)
* [Legislation and compliance](/references/legislation-and-compliance.md)
* [Transactional messaging](/foundations/transactional-messaging.md)
* [Copywriting](/foundations/copywriting.md)
