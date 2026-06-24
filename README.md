# Sewaka – Caregiver Support Platform

Final project for the [Building AI](https://buildingai.elementsofai.com) course

## Summary

Sewaka is a Bahasa Indonesia web platform for family caregivers of elderly relatives at home. It screens for caregiver burnout (ZBI-12) and depression (PHQ-2), offers condition-specific resource guides, and provides an AI assistant — Tanya Sewaka — to answer caregiving questions.

Live: [sewaka-app.sewakacare.workers.dev](https://sewaka-app.sewakacare.workers.dev)

## Background

When an elderly person is discharged from hospital in Indonesia, their family goes home with a diagnosis and almost nothing else. There's no structured handoff for the people who will actually do the caregiving — typically a spouse or adult child with no clinical background, no training, and no one to call when things get difficult.

I built Sewaka because this gap is real, it's common, and the tools that exist to address it (validated caregiver assessments, structured psychoeducation, accessible health information) simply aren't reaching the people who need them. They're locked inside clinical research, written in English, or buried behind healthcare systems that working families can't navigate.

The specific problems:

* Family caregivers frequently experience burnout and depression without recognising it or having a name for it. The ZBI-12 and PHQ-2 are well-validated tools for this — they just aren't being offered to caregivers outside of research settings.
* Health information about stroke, dementia, and Parkinson’s disease is rarely available in Bahasa Indonesia at a literacy level that ordinary families can use.
* The questions that come up when you're caring for someone at home — what does this symptom mean, is this normal, what should I do tonight — have nowhere to go.

## How is it used?

The platform is designed to be used at home, on a phone, in the days and weeks after a hospital discharge. A discharge nurse introduces it to the family before they leave the ward.

The caregiver completes the ZBI-12 and PHQ-2 assessments (about 5 minutes), selects the primary condition they're managing, and then has access to resource guides tailored to that condition. From there they can use Tanya Sewaka — the AI assistant — to ask questions in plain Bahasa Indonesia.

Tanya Sewaka is grounded in a curated, reviewed knowledge corpus. It doesn't retrieve from the open web and it doesn't try to replace a doctor. It's designed to be the kind of clear, patient answer a well-informed nurse might give at the end of a busy shift — if they had time.

## Challenges

The biggest challenge isn't technical — it's clinical legitimacy. An AI-assisted health tool in Indonesia has to earn the trust of clinical partners before it can reach real users. Getting a geriatrician or specialist nurse to co-review the content, agree to be cited, and put their name adjacent to the output is hard to do quickly as an independent developer.

There's also the hallucination problem. LLMs will generate plausible-sounding but wrong information, and in a health context that's serious. I've addressed this through a fixed, version-controlled corpus (not live web retrieval) and strict prompt guardrails — but I also caught a fabricated source attribution during development, which was a useful reminder that this requires active governance, not just good initial design.

Privacy is another real constraint. Caregiver burden scores and depression screens are sensitive. The platform is built without cookie-based tracking or advertising analytics, in keeping with Indonesian data protection law (UU PDP No. 27/2022). Assessment responses aren't retained beyond the session.

The ethical boundary I think about most: caregivers shouldn't use this instead of talking to a doctor. The platform includes clinical handoff prompts, but I can't control how people use it, and I can't know how distressed someone is when they open it at midnight. That's a limit I have to be honest about.

## Data sources

Sewaka doesn't train a model. Tanya Sewaka uses the Claude API, and the knowledge it draws on comes from a curated corpus I assembled: 14 reviewed chunks drawn from Indonesian clinical guidelines, published caregiver support literature, and the psychometric frameworks behind the ZBI-12 and PHQ-2.

All sources are verified and attributed in a public repository: [Sewakacare/sewaka-corpus](https://github.com/Sewakacare/sewaka-corpus).

The corpus is pinned to reviewed git tags — unreviewed changes don't reach production. No caregiver data is used to train or update any model.

## What next?

The platform is built. What I can't do alone is the clinical part.

The corpus needs to be reviewed by a clinical partner — a geriatrician, specialist nurse, or palliative care team — before I'm comfortable putting it in front of real caregivers. That's the single thing that would move this forward most. I've drafted a reviewer guide and an export workflow to make the review as low-friction as possible, but I still need someone to say yes.

Beyond that: I'd benefit from UX input from someone with experience in designing for lower digital literacy, and eventually from support in structuring the pilot (ethics protocol, outcome measurement, data handling) in a way that satisfies what clinical partners would need to see.

The technology is the part I can handle. The rest requires people I haven't found yet.

## Acknowledgments

* [Anthropic](https://anthropic.com) — Claude API powering Tanya Sewaka
* [Cloudflare Workers](https://workers.cloudflare.com) — platform hosting
* Steven H. Zarit — Zarit Burden Interview (ZBI-12)
* Spitzer et al. — Patient Health Questionnaire (PHQ-2)
* Reaktor Innovations & University of Helsinki — Building AI course
