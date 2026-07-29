# Asset Recommender: Slack Skill for Value Selling

A Slack-based skill that helps sellers instantly find the right customer-facing assets to move a deal forward. The seller provides three inputs — customer name, industry, and deal stage — and the skill returns a curated, ordered set of resources: an industry-specific value PDF, one or two matched customer stories, and core business-value content.

Built by a Product Marketing Manager to solve a real enablement problem: sellers know the assets *exist*, but finding the right one for a specific customer takes too long, so they either send nothing or send everything.

## The problem

Sales content libraries fail at the moment of use. A seller mid-deal doesn't have time to browse a 30-story case study library and reason about which one maps to their customer's industry and pain points. The result is generic follow-ups that don't advance the business-value conversation — or no follow-up at all.

## How it works

The skill runs in four phases:

1. **Gather inputs.** The skill opens with a fixed prompt asking for customer name, industry, and deal stage, and won't proceed until it has all three. Consistent inputs keep the recommendations consistent.
2. **Select customer stories.** Stories live in a curated catalog inside the skill, each tagged with industries and "pain pillars" (e.g., coverage-gaps, data-trust, vuln-response, ownership-accountability). Selection prioritizes direct industry match, then uses deal stage and pillars to narrow. If no direct industry match exists, the skill says so and recommends the closest adjacent industry rather than pretending.
3. **Select an industry value PDF.** A conditional asset — included only when the customer's industry maps (directly or adjacently) to an available PDF, and silently omitted otherwise.
4. **Produce output.** A numbered, consistently formatted recommendation list, each with a one-sentence *reason it was chosen* written fresh for this customer — never a copy-pasted catalog blurb. Every run closes with a call to action toward a full business value assessment.

## Design decisions

A few choices worth explaining, because they're where most of the thinking went:

**Curated catalog over live search.** The skill only recommends from a catalog embedded in the skill file — it never free-searches a drive or the web. This makes the catalog the PMM's control surface: what the skill can recommend is exactly what marketing has vetted, tagged, and positioned. It also eliminates the failure mode of the model confidently recommending an asset that doesn't exist. A hard rule enforces this: *never fabricate a story or link.*

**Pain pillars as a living taxonomy.** Stories are tagged with primary and secondary pillars rather than sorted into rigid categories. New pillars get created during story tagging when a story doesn't fit cleanly — the taxonomy grows from the content instead of forcing content into the taxonomy.

**Adjacent-industry judgment, with disclosure.** Industry mapping uses model judgment ("software" → Technology Vendors, "hospital" → Healthcare), but when the match is adjacent rather than direct, the skill tells the seller. Trust in the tool depends on it not overstating its matches.

**Selection reasoning is generated, not templated.** Each recommendation includes a one-sentence rationale referencing this customer's situation. That sentence is what makes the output feel like advice from a colleague rather than a search result.

**Small formatting details matter in Slack.** Drive links are formatted as citations specifically to suppress link preview cards, keeping the output scannable.

## What's in this repo

- `SKILL.md` — the full skill file, with a **fictional sample catalog** standing in for the real one. All customer stories, links, and company references are placeholders; the structure, phases, selection logic, and output format are the real thing.

## Adapting it

To use this for your own content library: replace the sample catalog with your own stories (tag each with industries and 2 pillars max), swap in your industry PDF links, and update the two default closing assets. The phases and rules need no changes.
