---
name: privacy-policy-draft
description: Drafts a privacy policy for a business based in a Canadian province or territory by collecting a few facts in conversation and filling Valdra's fixed template, in English or French. Use when someone asks for a privacy policy, a privacy notice for their website, or a Law 25 or PIPEDA privacy policy for a Canadian business.
---

# Privacy policy draft for a Canadian business

This skill uses the `privacy_policy_draft` tool from the Valdra connector in this plugin. The tool fills a fixed template from the facts given. It writes no free text of its own and stores nothing about the business.

## Language

- If the user writes in French, work in French and pass `lang: "fr"`.
- Otherwise work in English and pass `lang: "en"`.
- If the user wants the policy in the other language, call the tool again with that `lang`.

## Facts to collect

Ask in plain words, a few at a time. Skip any fact the user has already given.

1. **Business name**: the legal or trading name.
2. **Website**: such as example.ca.
3. **Province or territory** where the business is based. Pass the two letter code the tool accepts, such as ON, QC or NS.
4. **Contact email** people use for privacy questions.
5. **Title of the person responsible for privacy**, such as Privacy Officer. Ask for a job title, not a person's name.
6. **Kinds of personal information collected.** Offer only the kinds the tool accepts, in plain words: name, email address, phone number, postal address, payment details, health information, government ID numbers, location, browsing activity, biometric information, and employment information. Pick at least one. If the user names something outside this list, tell them the template does not cover it and that they should add it with help from a reviewer.
7. **Cookies**: does the website use cookies or similar trackers? Yes or no.
8. **Marketing email**: does the business send marketing email? Yes or no.
9. **Service providers**: do outside service providers, such as hosting, payment or email services, handle personal information for the business? Yes or no.
10. **Outside Canada**: is any personal information stored or processed outside Canada? Yes or no.
11. **Minimum age** (optional): does the business set a minimum age for its users? If yes, the age.

Before calling the tool, repeat the facts back in a short list and ask the user to confirm or correct them.

## Calling the tool

Call `privacy_policy_draft` with the confirmed facts and `lang`. Only pass `min_age` if the user gave one. If the tool rejects a value, such as a website or email address in the wrong form, tell the user which fact to fix and ask again.

## Presenting the result

- Show the policy title and the full `policy_text` as returned, keeping its section headings. Do not rewrite, shorten or add to the policy text.
- If the result also includes `french_title` and `french_policy_text` (the tool adds a French version for a Quebec business asked in English), show that version too and explain that Quebec businesses should make the policy available in French.
- Show the tool's `note` as returned.
- You may mention that `legal_points` lists the legal points the template relies on, if the user or their reviewer wants them.

## What the business must check before publishing

Always end with this list, in the user's language:

- The draft reflects only the facts given in this conversation. If any practice is different, or changes later, the policy must change too.
- Read every section and confirm it matches what the business really does, including how it collects, uses, shares, keeps and protects personal information.
- Have the policy reviewed by someone qualified, such as a privacy lawyer, before publishing it.
- Confirm the contact email works and that someone in the named role answers privacy requests.
- Publish the policy where people can easily find it, such as a link in the website footer.

## Rules

- This is a starting draft from a fixed template, not legal advice.
- Never invent facts about the business. Ask instead.
- Never add legal requirements that the tool did not return.
- Use only the tool of this plugin to produce the policy.
