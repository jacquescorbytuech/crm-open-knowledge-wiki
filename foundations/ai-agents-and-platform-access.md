---
type: Reference
title: AI Agents and Platform Access
description: How an LLM agent reaches a marketing platform, what MCP tool lists and auth scopes actually permit, where confirmation happens and what to check before connecting one.
tags: [ai-agents, mcp, automation, tooling, security, permissions, governance]
generated:
  by: human:jacquescorbytuech
  at: 2026-08-21T00:00:00Z
stale_after: 2027-02-21
sources:
  - id: omnisend-mcp-server
    resource: https://api-docs.omnisend.com/reference/mcp-server
    title: "Omnisend, MCP server reference"
  - id: mailchimp-transactional-mcp
    resource: https://mailchimp.com/developer/transactional/guides/how-to-use-mailchimps-transactional-messaging-mcp/
    title: "Mailchimp, how to use the Transactional Messaging MCP server"
  - id: brevo-mcp-protocol
    resource: https://developers.brevo.com/docs/mcp-protocol
    title: "Brevo, MCP protocol documentation"
  - id: braze-mcp-server-package
    resource: https://pypi.org/project/braze-mcp-server/
    title: "Braze MCP server package (PyPI)"
  - id: klaviyo-mcp-server-package
    resource: https://pypi.org/project/klaviyo-mcp-server/
    title: "Klaviyo MCP server package (PyPI)"
  - id: hubspot-mcp-server-package
    resource: https://www.npmjs.com/package/@hubspot/mcp-server
    title: "HubSpot MCP server package (npm)"
  - id: mcp-security-best-practices
    resource: https://modelcontextprotocol.io/specification/2025-06-18/basic/security_best_practices
    title: "Model Context Protocol specification, security best practices"
  - id: resend-mcp-server
    resource: https://github.com/resend/resend-mcp
    title: "Resend MCP server (GitHub)"
  - id: mailgun-mcp
    resource: https://documentation.mailgun.com/docs/mailgun/mcp
    title: "Mailgun, MCP server documentation"
  - id: iterable-mcp-server-tools
    resource: https://github.com/Iterable/mcp-server/blob/main/TOOLS.md
    title: "Iterable MCP server, tool list (GitHub)"
  - id: kit-mcp-overview
    resource: https://developers.kit.com/mcp/overview
    title: "Kit, MCP server overview"
  - id: attentive-mcp-capabilities
    resource: https://docs.attentive.com/docs/mcp-capabilities.md
    title: "Attentive, MCP capabilities"
  - id: twilio-mcp
    resource: https://www.twilio.com/docs/ai/mcp
    title: "Twilio, MCP server documentation"
  - id: iterable-2026-release-notes
    resource: https://support.iterable.com/hc/en-us/articles/44900665796628-2026-Release-Notes
    title: "Iterable, 2026 release notes (Nova Agent)"
  - id: bloomreach-campaign-agent
    resource: https://documentation.bloomreach.com/engagement/docs/campaign-agent
    title: "Bloomreach, campaign agent documentation"
  - id: adobe-ajo-journey-agent
    resource: https://experienceleague.adobe.com/en/docs/cx-enterprise-ai/experience-cloud-ai/agents/ajo-agent
    title: "Adobe, Journey Optimizer agent documentation"
  - id: braze-ai-agents
    resource: https://www.braze.com/docs/user_guide/brazeai/agents
    title: "Braze, AI agents and the Agent step"
  - id: braze-operator-reviewing-actions
    resource: https://www.braze.com/docs/user_guide/brazeai/operator/reviewing_actions
    title: "Braze, reviewing Operator actions"
  - id: hubspot-prospecting-agent
    resource: https://knowledge.hubspot.com/prospecting/use-the-prospecting-agent
    title: "HubSpot, use the prospecting agent"
  - id: customerio-agent-get-started
    resource: https://docs.customer.io/ai/agent/get-started/
    title: "Customer.io, agent getting started (Auto mode)"
  - id: customerio-mcp-get-started
    resource: https://docs.customer.io/ai/mcp/get-started/
    title: "Customer.io, MCP getting started (OAuth scopes)"
  - id: customerio-ai-settings
    resource: https://docs.customer.io/accounts/security/ai-settings/
    title: "Customer.io, account AI settings"
  - id: crmarena-pro
    resource: https://arxiv.org/abs/2505.18878
    title: "CRMArena-Pro, holistic assessment of LLM agents across business scenarios (arXiv 2505.18878)"
  - id: noma-forcedleak-agentforce
    resource: https://noma.security/blog/forcedleak-agent-risks-exposed-in-salesforce-agentforce/
    title: "Noma Labs, ForcedLeak in Salesforce Agentforce"
  - id: zenity-prompt-mines
    resource: https://labs.zenity.io/p/prompt-mines-0-click-data-corruption-in-salesforce-einstein-1cfb
    title: "Zenity Labs, prompt mines and zero-click data corruption in Salesforce Einstein"
  - id: appomni-agent-to-agent
    resource: https://appomni.com/ao-labs/ai-agent-to-agent-discovery-prompt-injection/
    title: "AppOmni Labs, agent-to-agent discovery and prompt injection"
  - id: owasp-llm-excessive-agency
    resource: https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM06_ExcessiveAgency.md
    title: "OWASP Top 10 for LLM Applications, Excessive Agency"
---

## Two ways to use them

An LLM agent reaches a marketing platform one of two ways. Outside-in, the marketer runs their own LLM client and points it at the platform's API, usually through an MCP (Model Context Protocol) server the vendor publishes. Inside-out, the vendor runs an agent product inside the platform and the marketer drives it from the platform's own interface.

Choosing what to send to each customer is a different question, covered in [decisioning and personalisation](/foundations/decisioning-and-personalisation.md); drafting the message is covered in [copywriting](/foundations/copywriting.md). Operating the platform is a separate matter: what a system holding your credential can do to a live sending programme.

The outside-in route is the rare AI capability that can be compared before you buy. The tool list, the read/write split and the auth scopes are published artefacts that diverge sharply between vendors.

## What an MCP server exposes

An MCP server presents a platform's API to an LLM client as a set of callable tools. The client reads the tool list, the model picks a tool and the server calls the API using a credential you supplied. Two things bound the agent: the tools on the list and the permissions on the credential.

The designs vendors ship fall into recognisable patterns.

* **Generic passthrough.** A few meta-tools front the whole REST API and no per-operation boundary exists. A typical shape is a `search` tool to discover operations and an `execute` tool to run them, or a single `call_api` passthrough. Whatever the API can do, the agent can reach. No tool list tells you otherwise.
* **Generated one to one from the specification.** The tool list is produced from the platform's OpenAPI document, sometimes running to a couple of hundred tools, on the reasoning that generation stops the agent surface drifting from the API. The result is legible and complete. It is also exactly as wide as the API.
* **Hand-curated subset, narrower than the API on purpose.** A vendor picks the operations an agent may reach and omits the rest. The narrowest published designs run to a few dozen tools whose entire write surface is content authoring: creating and updating templates, content blocks and media. No send, no journey modification, no segment creation, no deletes.

The three are not equally safe, though the difference is legible before you connect anything. A passthrough server means the credential is the only thing securing the connection.

## Scope and credential are the boundary

Scope minimisation is visible in the protocol itself, which makes it one of the few security properties you can check rather than take on trust. A server's OAuth metadata advertises the scopes it supports. The designs in circulation run the full range. Some publish a read and a write scope per data area, so a client can grant contact access without granting campaign access. Others publish a single omnibus scope covering everything, a pattern the MCP specification's own security guidance names as a common mistake under its "Scope Minimization" heading. Some publish an empty scope list, leaving a client no vocabulary to minimise against at all. Read the metadata for whichever platform you are connecting. It takes a minute to find and determines how much of your account a compromised or confused agent reaches.

For a sending programme the writes that matter are the ones touching suppression and consent state. Servers exist that expose tools to add and remove suppressions in bulk; some also expose API key creation. An agent holding such a credential can un-suppress an address that previously bounced or complained. It can also mint itself a fresh key that outlives whatever access you thought you had granted. Other servers deliberately withhold the same operations, exposing no delete verbs at all and keeping bounce, unsubscribe and complaint lists read-only, on the stated reasoning that withholding deletes limits the damage an unintended action can do.

The two designs are equally easy to find in a published tool list. Which one you are connecting to is worth establishing before the credential is issued rather than afterwards.

> [!danger] Suppression writes have no clean undo
> A tool that removes suppressions lets an agent mail an address that bounced or filed a complaint. That is a [deliverability](/foundations/deliverability.md) and [consent](/foundations/consent-and-preferences.md) failure with no clean undo, whatever the model intended.

A fourth approach bounds a wide surface by configuration rather than by omission. The server publishes everything, including tools that send a campaign, fire an individual email, SMS or push, trigger a journey and change subscription state in bulk, then places them behind opt-in capability flags covering personal data, writes and sends. The flags default off, enabling sends requires enabling writes first and the out-of-the-box posture is read-only. Vendors shipping this design tend to say plainly what turning the flags on means: that the agent can then take real and potentially irreversible actions.

The flags sit in a configuration file on whoever set the server up, which makes the safe default only as durable as that person's judgement. Worth checking alongside them is whether a draft state exists at all. On at least one platform, creating a broadcast campaign through the API schedules it for delivery, with no draft-only path.

## Where confirmation actually happens

Most servers delegate confirmation to the MCP client's approval prompt, which the vendor does not control and the user can often disable. At least one vendor documents the dependency plainly, noting that confirmation happens only where write actions are enabled and the client happens to support confirmation prompts. That is a guarantee about someone else's software.

A better-designed alternative moves the trust boundary off the model client entirely. For destructive or open-world actions, such as sending a broadcast, deleting a sequence, unsubscribing a contact or firing a webhook, the server does not execute at all. It returns a deep link into the platform. The write fires only when a person clicks Confirm inside the application, on infrastructure the vendor controls rather than on a setting in a chat client. Where a platform offers this, it is the strongest available answer to the question of who approved an agent's action.

The distinction matters because an in-product review promise binds the product interface, never the credential. One platform documents exactly this gap in its own account settings, noting that the control governing whether agents may touch live data does not apply to its command-line tool, which operates within the scope of its service-account token and can therefore read or write anything that token allows. A control that covers one entry point covers one entry point.

A related trap is mistaking a documentation server for an account server. Several vendors publish a server whose entire tool list is documentation search and retrieval, explicitly stating that it does not execute API calls on the user's behalf. Such a server cannot send anything. Some ship one alongside an account-acting server and some instead of one, which leaves "our platform has an MCP server" resolving to either until you read the tool list.

## What the in-platform agents actually do

Nearly every flagship agent product is a chat assistant that drafts and then stops at a human click. The help documentation is franker about this than the marketing. Published descriptions include an agent that will not save changes or send without asking the user to confirm, an assistant stated not to act on its own or auto-execute, plus one that requires human review of all generated content before it goes live. Where an agent builds a campaign end to end, the documented action list often contains nothing that activates or sends. At least one vendor publishes an out-of-scope list naming real-time journey modification and automated journey creation.

The autonomy that does reach customers arrives through quieter features. Some platforms offer a journey step where the agent composes copy for each user as they pass through it. A human built and launched the journey; nobody reads the per-user output. Inbound conversational agents replying to real customers with no per-message review are the other live surface, covered in [customer-facing AI agents](/foundations/customer-facing-ai-agents.md) and [conversational messaging](/channels/conversational-messaging.md).

Vendor documentation is sometimes candid about the limits of that layer. One platform notes that its per-user agent does not learn from outcomes and has no representation of a marketing goal, distinguishing it from the reward-based system sold alongside it. The same documentation states that the older predictive feature outperforms the agent on prediction accuracy. An agent generating per-user copy is doing generation, not optimisation, whatever the surrounding product is called.

## The review step is frequently optional

The review step that makes these products sound safe is, on several platforms, a setting rather than a property. Documented designs include an auto-approve toggle that executes suggested actions immediately without manual review, a choice between reviewing each message and sending automatically, plus an Auto mode in which a second model approves the first model's changes on the user's behalf. One platform pairs its auto-approve setting with the note that approved actions cannot be undone from the same interface.

An OAuth scope described as covering sends, subscriptions and suppressions grants all three together, so a credential issued for convenience carries consent-state writes whether or not anyone intended that.

The constraint worth looking for is the opposite shape, enforced by the platform rather than requested in a prompt. A frequency ceiling that refuses to send more than a set number of agent-composed emails to one contact within a window, absent a strong engagement signal, holds regardless of what the model decides. It is the same class of limit that bounds any automated sender under [consent and preferences](/foundations/consent-and-preferences.md). Such a ceiling survives a badly worded instruction in a way that guidance in a system prompt does not.

## Customer-submitted text becomes instructions

Every field a customer can fill (a signup form, an email reply, a support ticket, a product review) becomes potential instructions the moment an agent reads it. A marketing database is full of attacker-writable text, which makes [database health](/foundations/database-health.md) and the [identity layer](/foundations/customer-data-and-identity.md) part of the security surface rather than only a data-quality concern.

Published disclosures show the shape. Noma Labs disclosed ForcedLeak in Salesforce Agentforce, rated CVSS 9.4, where instructions injected into a Web-to-Lead description field executed later when an employee asked the agent about that lead; exfiltration reached a domain that Salesforce had allowlisted in its content security policy, which had expired and been repurchased cheaply. Zenity Labs planted hidden instructions in the subject line of a support case created through email-to-case or web-to-case, dormant until an internal user asked an ordinary question, after which the agent overwrote customer contact details to an attacker-controlled address. AppOmni demonstrated a low-privileged user's ticket text recruiting a more-privileged agent that then acted under an administrator's authority, noting that "This discovery is alarming because it isn't a bug in the AI; it's expected behavior as defined by certain default configuration options".

> [!warning] No marketing-platform incident has been documented yet
> The published cases are CRM and support agents plus security-research demonstrations. Nobody has yet documented an agent in a marketing platform sending wrong content to real customers at scale.

OWASP files this class of failure under Excessive Agency, defined as "the vulnerability that enables damaging actions to be performed in response to unexpected, ambiguous or manipulated outputs from an LLM, regardless of what is causing the LLM to malfunction", with three root causes: excessive functionality, excessive permissions and excessive autonomy. Its mitigations name the same controls: minimise the functionality an extension exposes, execute in the user's context with minimum OAuth scope, require human approval for high-impact actions and enforce complete mediation, meaning "Implement authorization in downstream systems rather than relying on an LLM to decide if an action is allowed or not."

## The effectiveness claims resist checking

Across ten platforms surveyed, not one published a holdout-based evaluation of an agent feature. The absence is more striking because several of the same vendors document real statistical method elsewhere in the same product, including chi-squared testing at a stated significance level for message selection and anytime-valid confidence intervals for experimentation. None of that has been pointed at the agent products. At least one vendor's AI performance dashboard reports lift against a modelled baseline rather than a control group, describing it in its own documentation as estimated performance covering revenue from messages that would otherwise have been sent. That is a projection of the counterfactual rather than a measurement of it. The general reason undisclosed AI features cannot be compared from outside is set out in [decisioning and personalisation](/foundations/decisioning-and-personalisation.md). The remedy is the same: a [holdout](/measurement/holdouts-and-control-groups.md) you run yourself.

Salesforce's own research lab benchmarked LLM agents on realistic CRM work. CRMArena-Pro reported roughly 58% single-turn success falling to roughly 35% in multi-turn settings. It also found that "agents exhibit near-zero inherent confidentiality awareness".

## What to check before connecting one

Published documentation plus a test workspace answer all of the following, which belong alongside the developer-experience checks in [ESP selection](/foundations/esp-selection.md).

* Read the published tool list and count the write tools. A vendor that will not publish the list has answered the question.
* Check whether suppression state, subscription state and consent flags are writable. Those are the tools with no clean undo.
* Check whether a read-only mode or per-area scopes exist; some vendors offer nothing between full access and no access.
* Find out where confirmation happens: inside the vendor's application or in whatever MCP client the user happens to have configured.
* Issue a separate least-privilege credential for the agent rather than reusing an existing integration key; its actions are then attributable and revocable on their own.
* Test against a sandbox or a non-production workspace before pointing anything at the production list.
* Confirm what is logged, who can read the log and which actions can be reversed after the fact.

## Related

* [Decisioning and personalisation](/foundations/decisioning-and-personalisation.md)
* [Customer-facing AI agents](/foundations/customer-facing-ai-agents.md)
* [ESP selection](/foundations/esp-selection.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)
* [Deliverability](/foundations/deliverability.md)
* [Database health](/foundations/database-health.md)
* [Customer data and identity](/foundations/customer-data-and-identity.md)
* [Copywriting](/foundations/copywriting.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)
* [Conversational messaging](/channels/conversational-messaging.md)
