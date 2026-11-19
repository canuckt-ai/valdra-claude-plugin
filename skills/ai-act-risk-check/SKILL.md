---
name: ai-act-risk-check
description: Screens an AI system under the EU AI Act by asking the yes or no facts that matter for the user's use case, then explains the risk tier, the obligations with their articles and dates, and other AI laws that may apply, such as in Canada, Ontario, Quebec, the US or the UK. Use when someone asks whether the EU AI Act applies to their AI tool, what risk tier it falls in, or what they must do as a provider or deployer. Works in English or French.
---

# EU AI Act risk check

This skill uses the `ai_act_risk_classify` tool from the Valdra connector in this plugin. The tool applies fixed rules to yes or no facts and returns a risk tier (prohibited, high, gpai, limited or minimal), the reasons, the obligations with their articles, and other AI laws that may also apply.

## Language

- If the user writes in French, work in French and pass `lang: "fr"`.
- Otherwise work in English and pass `lang: "en"`.

## Steps

1. **Understand the use case.** Ask the user to describe in a sentence or two what the AI system does, who it affects, and where it is used. Keep a short plain summary to pass as `use_case`.
2. **Ask about the role.** Ask whether their organization builds the system or sells it under its own name (provider), uses it under its own authority (deployer), or both. If they use someone else's system, also ask whether they put their own name on it or change it substantially, since that can make them the provider.
3. **Ask only the relevant yes or no facts.** Read the descriptions of the tool's yes or no fields and ask only those that could fit the use case, a few at a time, in plain words. For example, a hiring tool calls for the questions on recruitment and worker monitoring and on inferring emotions at work; a chatbot calls for the questions on interacting with people and generating content. Always check the prohibited practices that could plausibly apply to the use case. Leave out facts that clearly do not apply; the tool treats them as no.
4. **Ask where it is used** and which groups of people its decisions affect, and map the answers to the `jurisdictions` and `affects` values the tool accepts.
5. **Confirm.** Repeat the facts back in a short list and ask the user to confirm or correct them.
6. **Classify.** Call `ai_act_risk_classify` with the confirmed facts, `use_case`, `jurisdictions`, `affects` and `lang`.

## Explaining the result

Use only what the tool returns:

- **Tier**: state the `risk_tier` and explain what it means in plain words.
- **Why**: summarize the `reasons`, keeping every article and date exactly as returned.
- **Role**: say which role the user confirmed, and point out the obligations the result marks for that role, such as those titled for a deployer. Mention when the result says a deployer can become the provider.
- **What to do**: list each item in `obligations` with its `article`, its title and a plain summary. Keep articles and dates exactly as returned.
- **Other laws**: list each item in `other_laws` with its jurisdiction, the law, whether it is in force, and its summary.
- **Note**: show the tool's `note` as returned.

## Rules

- This is a screening from fixed rules, not legal advice. Say so, and suggest a qualified lawyer for a final view, especially for a prohibited or high tier.
- Never invent an obligation, an article, a date or a law that the tool did not return. If the user asks about something the result does not cover, say so.
- If the user's facts change, call the tool again rather than adjusting the result yourself.
- Use only the tool of this plugin for the classification.
