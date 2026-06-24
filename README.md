# Sewaka – Caregiver Support Platform

Final project for the [Building AI](https://buildingai.elementsofai.com) course

## Summary

Sewaka is a Bahasa Indonesia platform that helps family caregivers of elderly relatives at home: a burnout and depression screener, condition-specific resource guides, and an AI assistant called Tanya Sewaka for follow-up questions.

Live: [sewaka-app.sewakacare.workers.dev](https://sewaka-app.sewakacare.workers.dev)

## Background

When an elderly person is discharged from hospital in Indonesia, their family goes home with a diagnosis and almost nothing else. There's no structured handoff for the people who will actually do the caregiving (typically a spouse or adult child with no clinical background, no training, and no one to call when things get difficult).

I built Sewaka because this gap is real, it's common, and the tools that exist to address it simply aren't reaching the people who need them. Validated caregiver assessments, psychoeducation materials, accessible health information in Bahasa Indonesia: all of it exists, mostly locked inside clinical research or buried behind healthcare systems that working families can't navigate.

The specific problems:

* Family caregivers frequently experience burnout and depression without recognising it or having a name for it. The ZBI-12 and PHQ-2 screen for this; they just aren't being offered to caregivers outside research settings.
* Health information about stroke, dementia, and Parkinson's disease is rarely available in Bahasa Indonesia at a literacy level ordinary families can use.
* The questions that come up when caring for someone at home (what does this symptom mean, is this normal, what should I do tonight) have nowhere to go.

## How is it used?

The platform is for use at home, on a phone, in the days and weeks after a hospital discharge. A discharge nurse introduces it to the family before they leave the ward.

The caregiver completes the ZBI-12 and PHQ-2 assessments (about 5 minutes), selects the primary condition they're managing, and gets access to resource guides tailored to that condition. From there they can ask Tanya Sewaka questions in plain Bahasa Indonesia.

Tanya Sewaka works from a curated, reviewed knowledge corpus. It doesn't fetch from the open web or try to replace a doctor. The goal is to give the kind of clear, patient answer a well-informed nurse might give at the end of a busy shift, if they had time.

## Challenges

Clinical legitimacy is the hard part, not the technical side. An AI-assisted health tool in Indonesia has to earn the trust of clinical partners before it can reach real users. Getting a geriatrician or specialist nurse to co-review the content, agree to be cited, and put their name next to the output is hard to do quickly as an independent developer.

LLMs also generate plausible-sounding but wrong information, and in a health context that's serious. I addressed this through a fixed, version-controlled corpus (not live web retrieval) and strict prompt guardrails. I still caught a fabricated source attribution during development, which was a useful reminder that active governance matters more than good initial design.

Privacy matters too. Caregiver burden scores and depression screens are sensitive. The platform runs without cookie-based tracking or advertising analytics, in line with Indonesian data protection law (UU PDP No. 27/2022). Assessment responses aren't stored beyond the session.

The ethical limit I keep coming back to: caregivers shouldn't use this instead of talking to a doctor. The platform includes clinical handoff prompts, but I can't control how people use it, and I can't know how distressed someone is when they open it at midnight.

## Data sources

Sewaka doesn't train a model. Tanya Sewaka uses the Claude API and draws on a corpus I assembled: 14 reviewed chunks from Indonesian clinical guidelines, caregiver support literature, and the source materials behind the ZBI-12 and PHQ-2. Sources are verified and listed in a public repository: [Sewakacare/sewaka-corpus](https://github.com/Sewakacare/sewaka-corpus).

The corpus is pinned to reviewed git tags. Unreviewed changes don't reach production. No caregiver data goes into training or updating any model.

## What next?

The platform is built. What I can't do alone is the clinical part.

The corpus needs review from a clinical partner before I'm comfortable putting it in front of real caregivers. That's the single thing that would move this forward. I've drafted a reviewer guide and an export workflow to make the review as low-friction as possible, but I still need someone to say yes.

I'd also benefit from UX input from someone with experience designing for low digital literacy, and eventually from help structuring the pilot so it meets what clinical partners need to see (ethics protocol, outcome measurement, data handling).

The technology is the part I can handle. The rest requires people I haven't found yet.

## Acknowledgments

* [Anthropic](https://anthropic.com) — Claude API powering Tanya Sewaka
* [Cloudflare Workers](https://workers.cloudflare.com) — platform hosting
* Steven H. Zarit — Zarit Burden Interview (ZBI-12)
* Spitzer et al. — Patient Health Questionnaire (PHQ-2)
* Reaktor Innovations & University of Helsinki — Building AI course
