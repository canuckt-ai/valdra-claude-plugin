---
name: canadian-privacy-law-lookup
description: Finds the closest matching statements of federal, provincial and territorial Canadian privacy law for a question, such as breach reporting, consent, access requests, penalties or who a law applies to, each with its legal citation, the official source link and the date it was last checked. Use when someone asks what PIPEDA, Quebec Law 25, CASL, PHIPA or another Canadian privacy act requires. Works in English or French.
---

# Canadian privacy law lookup

This skill uses the `canadian_privacy_law_lookup` tool from the Valdra connector in this plugin. The tool searches Valdra's registry of Canadian privacy law statements and returns the closest matching statements as stored, each with its citation, the official source URL, the date the source was current to, and the date the statement was last checked against it.

## Language

- If the user writes in French, work in French and pass `lang: "fr"`.
- Otherwise work in English and pass `lang: "en"`.

## Steps

1. **Find the place.** If the question depends on where the organization operates and the user has not said, ask for the province or territory, or whether federal law is meant. Pass it as `jurisdiction` (`CA` for federal, or `CA-` and the two letter code, such as `CA-QC`). If the user wants all of Canada, leave it out.
2. **Pick the kind, when it is clear.** For a deadline question pass `kind: "deadline"`; for fines `kind: "penalty"`; for who the law covers `kind: "scope"`. Otherwise leave it out.
3. **Look it up.** Call `canadian_privacy_law_lookup` with a short `query` of the key words of the question, in the legal terms the law would use, such as "breach notification" or "consent for marketing email", not the whole question. Use the user's language: French words when `lang` is `fr`.
4. **No match.** If the result has no statements, try once more with the law's name or a plainer word, as the result's `no_match` text suggests. If there is still nothing, say the registry has no statement on it.

## Explaining the result

Use only what the tool returns:

- Answer the question in plain words from the `statement` of the most relevant results. The results are the closest matches in the registry, not a guaranteed answer: if none of them answers the question, say so.
- After each point give its `citation` exactly as returned and its `source_url` as a link.
- Say the date in `verified_on` when you give a deadline or a penalty.
- If `more_results` is true and the question is broad, offer to narrow it by province or kind.
- Show the tool's `note` as returned.

## Rules

- This is a reference to the law, not legal advice. Say so, and suggest a qualified lawyer for a decision.
- Never invent a section, a deadline, an amount or a source that the tool did not return. If the result does not answer the question, say so.
- Do not reword a statement in a way that changes its meaning; quote it when the exact words matter, such as a deadline.
- Use only the tool of this plugin for the law.
