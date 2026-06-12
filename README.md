# RecruiterOS

AI-powered CV scoring pipeline for recruitment agencies.

## What It Does
- Candidates submit CVs via branded form
- AI scores on 5 dimensions (impact, skill depth, growth, initiative, signal)
- Instant candidate feedback via email
- Agency sees ranked shortlist in clean dashboard
- Auto-purges CVs after 30 days for compliance

## Architecture
Tally → Airtable → Make.com → PDF.co → Groq → Gmail

## Core Flow
| Stage | Tool |
|-------|------|
| Trigger | Airtable Watch Records |
| CV URL | Set Variable |
| Text Extraction | PDF.co |
| AI Scoring | Groq (openai gpt-oss-20b) |
| JSON Parse | JSON Parser |
| Score Routing | Router (3 branches) |
| Data Write | Airtable Update |
| Status Transition | Airtable Update |
| Email Notifications | Gmail Inline |
| Auto-Purge | Scheduled Delete |

## Score Distribution (Test Batch)
- 92: Exceptional
- 68: Solid, early career
- 65: Solid, unremarkable
- 25: Professionalism fail

## Key Decisions
- Generic scoring (not job-specific) — agencies span industries
- Contextual > quantitative — junior with shipped SaaS > senior with "Employee of the Month"
- Inline emails — fewer credits, simpler mental model
- Auto-reject ≤25, review 50-70, shortlist 85+ — saves 50% recruiter time

## Stack
- **Form:** Tally.so
- **Database:** Airtable
- **Automation:** Make.com
- **Text Extraction:** PDF.co
- **AI:** Groq (openai gpt-oss-20b)
- **Email:** Gmail

## Demo
https://www.loom.com/share/9accb840c4414fd6a2652a607be70578

## Status
MVP complete. Piloting with agencies.

## Contact
OndialeCoded@gmail.com
