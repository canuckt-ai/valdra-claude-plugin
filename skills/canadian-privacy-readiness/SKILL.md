---
name: canadian-privacy-readiness
description: Runs Valdra's free Canadian privacy readiness check for a small organization (PIPEDA, Quebec Law 25, CASL and AI governance) as a plain yes or no conversation, then scores it and explains the top gaps and the step that closes each. Use when someone asks whether their business is compliant with Canadian privacy law, wants a privacy health check, or asks where to start with privacy in Canada. Works in English or French.
---

# Canadian privacy readiness check

This skill walks a small Canadian organization through Valdra's readiness check using two tools from the Valdra connector in this plugin: `privacy_readiness_questions` and `privacy_readiness_score`.

## Language

- If the user writes in French, work in French for the whole conversation and pass `lang: "fr"` to both tools.
- Otherwise work in English and pass `lang: "en"`.
- If the user switches language, switch with them and use the matching `lang` on the next call.

## Steps

1. **Get the questions.** Call `privacy_readiness_questions` with the user's language. Each question comes with an `id`, a `category`, the question text and the `law` it comes from. Keep the ids; you need them to score.
2. **Set expectations in one or two sentences.** Say this is a short yes or no screening of their privacy practices, that nothing they answer is stored by the scoring tool, and that it is not legal advice.
3. **Ask a few questions at a time.** Group them by category and ask two to four per message. Put each question in plain words the owner of a small business would understand, while keeping its meaning exactly the same. You may show the law reference in brackets for anyone who wants it.
4. **Record each answer as true or false.** Yes is `true`, no is `false`. If the user is unsure, explain the question once more in simpler words. If they still do not know, record `false`, since an unknown practice is usually not in place, and tell them you did so. If they prefer to skip a question, leave it out; the scoring tool leaves unanswered questions out of the score, so tell them the result will be less complete.
5. **Ask every question** before scoring, unless the user asks to stop early. A partial set of answers gives a partial picture.
6. **Score.** Call `privacy_readiness_score` with `answers` as a map of question id to true or false, and the user's `lang`.
7. **Explain the result** using only what the tool returns:
   - the `score` out of 100 and the `risk_level`;
   - the `category_scores`, pointing out the weakest categories;
   - each item in `top_gaps`: its category, its priority, and its `what_to_do` step, in plain words;
   - the `full_assessment_url`, offered as the link to Valdra's free full assessment.
8. **Offer a next step.** For example, if a gap is a missing privacy policy, offer to help draft one with the privacy policy draft skill in this plugin.

## Rules

- Never invent a legal requirement, a deadline, a penalty or a law reference that the tools did not return. If the user asks about something the tools do not cover, say that this check does not cover it and suggest they ask a qualified privacy lawyer or use the full assessment.
- Do not change the meaning of a question when you rephrase it.
- Present the result as a screening, not legal advice and not a certification of compliance.
- Use only the tools of this plugin for the check. Do not use other tools or outside sources to add requirements.
- Keep the tone calm and practical. A low score is a list of next steps, not a verdict.
