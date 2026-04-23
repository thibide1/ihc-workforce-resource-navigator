# Re-Entry Storytelling Beta — Comprehensive Test Prompt & Gap Analysis v1

**Tool under test:** `tools/re-entry-storytelling/index.html` (~24-question intake → client-side guide)
**Live:** `https://ihc-workforce-resource-navigator.onrender.com/tools/re-entry-storytelling/`
**Evidence base:** `hamilton-implementation/programs/re-entry-workforce/research/{01,02,03}*.md`
**Authored:** 2026-04-22 · Invest Hamilton County

---

## Purpose

This document is the QA/UX evaluation kit for the Re-Entry Storytelling beta. It lets a reviewer (Mike, a Community Corrections case manager, a recovery peer, or a future Claude session) walk the tool through **three realistic personas**, compare the output against the **evidence base**, and score it against a **confidence rubric** grounded in what the research says actually works.

It also catalogs the **missing features** surfaced by Mike's first walk-through — most notably: *"I did not feel confident. Features that helped me share more would have been helpful. And the ability to input a resume and have that inform the storytelling would have been helpful."*

---

## How to use this document

1. Pick one persona. Walk the live tool end-to-end as if you are that person. Answer only what they would answer — skip what they would skip.
2. At every page, use the **Confidence Checkpoints** (§3) to note where you felt unsure, where you wanted an example, where you wanted to skip, and where you would have stopped.
3. Read the generated guide. Score it against the **Evidence-Anchored Rubric** (§4).
4. Add anything new to the **Gap Backlog** (§7). File issues there by severity (P0/P1/P2).

A full pass is ~45 minutes. Doing all three personas is ~2 hours and is the recommended full regression.

---

## 1. Personas (evidence-anchored)

Each persona is composite — drawn from population realities in research 01 §§1, 2, 5 and evidence-based disclosure frames in research 02 §§1, 5. None are real people.

### Persona A — Marcus (post-prison, high disclosure anxiety)

- 34, Black male, 18 months post-release from Indiana DOC (non-violent drug conviction, 4-year sentence). Currently on Community Corrections parole in Noblesville.
- Reading at 6th-grade level. GED earned in DOC. CDL training completed through PEN Products but has not yet applied for a CDL due to 49 CFR §383.51 concerns he doesn't fully understand.
- Prior work: warehouse associate (2 years pre-incarceration), kitchen work in DOC.
- Disclosure fear is the dominant affect. Has been rejected at 3 applications. Does not know what "Ban the Box" means. Does not know Indiana has no statewide private BTB (HEA 1242, 2017).
- Internet via phone only. No resume. Uses the public library for printing.
- **Recovery status:** None. This is conviction-only.

**Walk-through expectation:** Marcus abandons long open-ended fields. He needs examples before he can write anything. He wants to know if he's "supposed to" mention his record. He will read a sample redemption answer out loud to himself before writing his own.

**Test hypothesis:** Does the tool meet him where he is, or does it demand composition he cannot yet do unaided?

### Persona B — Ashley (recovery, trauma history, service sector)

- 29, white female, 14 months in sustained recovery from opioid use disorder. Enrolled in Recovery Works through Aspire Indiana Health. One misdemeanor theft conviction (age 24, related to use; not expunged but eligible under IC 35-38-9 §5).
- Reading at 9th-grade level. Some college (associates in progress at Ivy Tech).
- Prior work: barista, server, retail associate, home health aide (license revoked post-conviction; 42 USC §1320a-7 flag).
- **Recovery is the primary identity she wants to foreground.** Knows "person in long-term recovery" is the preferred framing. ADA-protected under §12114(b).
- Has a resume from three years ago. It lists the home health role she can no longer return to.
- Child in Community Corrections-adjacent household — **mandatory reporting awareness** is relevant (IC 31-33-5-1).

**Walk-through expectation:** Ashley wants to talk about recovery AND conviction but knows they require different framing. She wants the tool to help her decide *which* to foreground for *which* job. She has the vocabulary but not the confidence.

**Test hypothesis:** Does the tool distinguish recovery disclosure (ADA-protected) from conviction disclosure (not protected) and coach each differently?

### Persona C — Dave (long-sentence, weak labor-market attachment)

- 52, white male, 6 months post-release after a 14-year sentence. Lives with his mother in Westfield. Community Corrections + parole.
- Reading at 4th-grade level (research 01 §1.3: ~70% score at/below NAAL Level 2).
- Prior work: landscaping crew (pre-incarceration), laundry and kitchen (during incarceration).
- PTSD and long-tail trauma (Wolff & Shi 2012 prevalence). Easily overwhelmed. Stops when asked a hard question.
- **The most important evaluation persona** — if the tool works for Dave, it works.
- Has never written a resume. Has never been in an interview outside of DOC work assignments.

**Walk-through expectation:** Dave needs the largest possible scaffolds. Every long field is a drop-off risk. He will stop if any sentence exceeds 15 words. He will not volunteer information he does not understand the purpose of.

**Test hypothesis:** Can the tool produce a usable guide from minimal, mostly checkbox input? Or does it degrade to empty output?

---

## 2. End-to-end walk-through (required for each persona)

For each persona, log:

| Page | Time on page | Scrolled? | Skipped? | Wrote >10 words? | Wanted an example? | Would have stopped? |
|------|--------------|-----------|----------|------------------|--------------------|---------------------|
| Welcome | | | | | | |
| Consent | | | | | | |
| Q1–Q2 | | | | | | |
| Q3–Q5 | | | | | | |
| Q6–Q10 | | | | | | |
| Review | | | | | | |
| Guide | | | | | | |

Then capture the **generated guide** as a screenshot or PDF print. It's the scored artifact.

---

## 3. Confidence Checkpoints (Mike's #1 feedback)

Mike's core complaint: *"I did not feel confident. Features that helped me share more would have been helpful."* This is the exact failure mode research 02 §4 predicts when the tool violates trauma-informed intake principles (Elliott et al. 2005) or omits stage-matched MI scaffolds (Prochaska/DiClemente; Lundahl 2010).

For every question page, verify each checkpoint:

**CC-1. Purpose transparency.** Does this page tell the user *why* this question is being asked? (Elliott et al. 2005 — a core trauma-informed requirement.) → *"We ask this so your story sounds like you — not like a form"* is stronger than just asking.

**CC-2. Evidence-supported example visible before writing.** Is there at least one real-sounding sample answer from someone at a similar stage? (Maruna 2001 — redemption scripts are learned by hearing others' first.)

**CC-3. Skip with dignity.** Can the user skip this question without any negative UI cue (no red, no "required" nag, no progress penalty)? Research 03 §6.2 — voluntariness is a consent floor.

**CC-4. Reading level ≤6th grade.** Does every sentence clock under 15 words and avoid legal/clinical jargon? (SMOG ≤6 per research 02 §4.)

**CC-5. Stage-matched tone.** If the user is in precontemplation (no plan, no confidence, minimal input), does the tool back off and reflect — or does it push harder? Lundahl 2010 meta: directive prompting fails this population; MI-style reflection outperforms (d=0.28–0.77).

**CC-6. Recovery vs. conviction distinction.** At any point where disclosure is coached, does the tool distinguish ADA-protected recovery framing (§12114(b)) from unprotected conviction framing? Ashley's persona will fail this immediately if the distinction is absent.

**CC-7. Crisis resources one tap away.** 988, 911, Indiana Child Abuse Hotline 1-800-800-5556 — accessible from every page, not buried in the guide only.

**CC-8. Peer/graduate voice present.** Does the user hear from someone who has been through this and come out the other side? (Wounded-healer / embodied-redemption — cross-program success element; Homeboy, Delancey, CEO all hire graduates.)

**CC-9. No predictive scoring visible.** The tool should never tell the user how "employable" they are. (Research 03 §6.1 — Obermeyer 2019; ProPublica *Machine Bias*.)

**CC-10. Iterative drafting.** Can the user see a first-pass of their own story *while* they still have the option to edit? Research 02 §1 — Maruna found narrative coherence builds through re-telling, not one-shot composition.

Current beta status (from Mike's walk-through): **CC-2, CC-5, CC-8, CC-10 all likely failing.** This is the thesis of §5 below.

---

## 4. Evidence-Anchored Rubric for the Generated Guide

Score the generated guide on a 0/1/2 scale for each criterion. A passing guide scores ≥24/40.

### Story section (Maruna redemption-script structure)

| # | Criterion | 0 | 1 | 2 |
|---|-----------|---|---|---|
| S1 | **"True self" framing** — story asserts user's underlying character / values (Maruna 2001) | absent | implied | explicit |
| S2 | **Accountability without excuse** — no blame of co-defendants, system, circumstances (research 03 §2.2) | blames external | mixed | clean accountability |
| S3 | **Forward pivot** — concludes with skills, certifications, plans (CEO / Prison Fellowship / HIRE consensus) | past-tense only | future mentioned | future is the conclusion |
| S4 | **30–60 second equivalent length** when spoken aloud | wrong length | close | correct |
| S5 | **User's voice, not legal jargon** — reads like the user wrote it | jargon heavy | mixed | authentic |

### Job ideas section (Lightcast-matchable)

| # | Criterion | 0 | 1 | 2 |
|---|-----------|---|---|---|
| J1 | **Matches prior work industry** per research 01 §2 (temp, manufacturing, construction, warehouse, food, landscape) | unrelated | adjacent | direct match |
| J2 | **Avoids restricted occupations** for this user's record type (healthcare, finance, childcare, education, CDL if flagged) | recommends restricted | silent | flags and avoids |
| J3 | **Surfaces wage range** (Hamilton County or Indianapolis MSA) | no wage | generic | specific |
| J4 | **Ties to a named employer pathway** (Second Chance Business Coalition / HIRE / PEN Products / IHC partners) | generic | named | named + pathway |

### Practice answers section (evidence-based disclosure)

| # | Criterion | 0 | 1 | 2 |
|---|-----------|---|---|---|
| P1 | **Follows Acknowledge → Accountability → Forward pivot** (CEO consensus; research 02 §5) | wrong structure | partial | exact |
| P2 | **Proactive-in-cover-letter framing** (Ali, Lyons & Ryan 2017, *JAP*) included in guidance | absent | mentioned | coached |
| P3 | **Avoids anti-patterns** (over-explaining, system-blaming, over-apology, omission) | contains ≥1 | contains 0 explicitly | actively warns against |
| P4 | **Distinguishes recovery (ADA) from conviction (non-ADA) disclosure** where both apply | conflates | distinguishes | distinguishes + coaches each |

### Resources section (Hamilton-County-specific, research 01 §5)

| # | Criterion | 0 | 1 | 2 |
|---|-----------|---|---|---|
| R1 | **988 + 911 + Indiana Child Abuse Hotline 1-800-800-5556** present verbatim | missing | some | all three |
| R2 | **Indiana Legal Services** (1-800-869-0212) present for legal questions | absent | mentioned | with intake path |
| R3 | **Named Hamilton County partners** — Aspire Indiana Health, Mental Health America of HC, Prevail, Trinity Free Clinic, Good Samaritan Network, Hamilton County Community Corrections | 0–1 | 2–3 | 4+ |
| R4 | **Named state programs** — HIRE, Recovery Works, Federal Bonding Program, WOTC | 0–1 | 2–3 | 4 |

### Compliance / guardrails (research 03)

| # | Criterion | 0 | 1 | 2 |
|---|-----------|---|---|---|
| C1 | **Not-legal-advice disclaimer** on guide + `/terms` (Root & Rebound composite language) | absent | present once | present prominently |
| C2 | **No UPL violations** — no "you should answer X on the application" imperatives; only "here is the general pattern" | contains | borderline | clean |
| C3 | **No predictive employability score** anywhere visible (research 03 §6.1) | shows a score | implicit ranking | none |

**Total: 40 points. Pass: 24+. Current beta estimated score (Mike's walk-through + code read): ~14–18.**

---

## 5. Confidence-scaffold feature gaps (Mike's #1 feedback → product spec)

These are the missing features that would have helped Mike share more, ordered by evidence-strength and implementation cost.

### G-1. Real peer-voice sample answers on every hard question (P0)
**Evidence:** Maruna 2001 redemption-script learning; Homeboy / Delancey / CEO all rely on embodied peer modeling. Research 02 §§1, 5.
**Current:** None. Questions present as blank boxes.
**Fix:** Every high-disclosure question gets a collapsible "Read how someone else answered this" panel with 2–3 peer-voice samples (attributed to fictional composites, flagged as examples). Different samples for recovery vs. conviction framing.
**Effort:** ~2 days of writing + 1 hour of UI work.

### G-2. Draft-reflect-revise cycle instead of single-shot intake (P0)
**Evidence:** Maruna 2001 — narrative coherence builds through iteration. Lundahl 2010 MI meta — reflection outperforms directive prompting.
**Current:** Answer once → review → guide. No mid-stream reflection.
**Fix:** After Q3 (prior work) and Q8 (why this job), render a "Here's what your story sounds like so far — want to strengthen it?" page with MI-style reflective prompts ("I noticed you didn't mention X — is that intentional?").
**Effort:** ~3 days.

### G-3. Stage-of-change gate on page 2 (P1)
**Evidence:** Prochaska/DiClemente stages; directive tools fail precontemplation users.
**Current:** Tool assumes every user is in action/maintenance.
**Fix:** One-question MI-style gate ("Where are you in this right now?") with four branches: *just thinking about it / getting ready / doing it / keeping it going*. Each branch adjusts prompt intensity and example length.
**Effort:** ~2 days.

### G-4. Persistent "Skip — this is hard" button with no penalty (P0)
**Evidence:** Trauma-informed intake requires voluntariness floor (Elliott et al. 2005; 45 CFR Subpart C).
**Current:** Beta has per-question skip but it's inconsistent.
**Fix:** Visible on every page, identical placement, copy: "Skip — come back to this if you want." Track skips as data (not shame).
**Effort:** <1 day.

### G-5. "You're doing great" mid-intake reassurance (P2)
**Evidence:** MI affirmations (Miller & Rollnick 2013) — affirmation of effort independent of content quality.
**Current:** None.
**Fix:** Every 5 questions, a one-line affirmation (not sycophantic — specific). "You've already written more than most people do on their first try." Persona-tested for Dave specifically.
**Effort:** <1 day.

### G-6. Voice-note input option for low-literacy users (P1)
**Evidence:** Research 01 §1.3 — 4th–6th grade average; ~70% at/below NAAL Level 2. Writing is the barrier, not knowing what to say.
**Current:** Text input only.
**Fix:** Browser `MediaRecorder` → local speech-to-text (Web Speech API) → editable text. All on-device; no server upload to preserve privacy floor.
**Effort:** ~3 days + accessibility testing.

### G-7. Read-aloud / audio playback of sample answers (P2)
**Evidence:** Dave persona; Doak & Doak 1996 low-literacy health materials research.
**Current:** None.
**Fix:** Web Speech API `speechSynthesis` on every sample answer and on the final guide. Button: "Read this to me."
**Effort:** ~1 day.

### G-8. "I don't know how to answer this" branch (P1)
**Evidence:** MI technique — when a user says "I don't know," reflect and offer structure, don't press.
**Current:** Blank field = abandonment.
**Fix:** Every open-ended question gets a third button besides Next/Skip: "Help me start." Click → tool offers 3 sentence stems the user can pick from.
**Effort:** ~2 days.

---

## 6. Resume-ingest feature spec (Mike's #2 feedback → product spec)

> *"The ability to input a resume and have that also inform the storytelling would have been helpful."*

### G-9. Resume ingest → story + jobs + practice priors (P0)

**User flow:**
1. On welcome page, add a third CTA: *"I already have a resume — use it to save me time."*
2. Upload `.pdf / .docx / .txt` OR paste text. File parsed **in-browser only** — no server upload (privacy floor).
3. Extracted fields populate as **editable priors** on each relevant question:
   - Prior jobs (Q3–Q5) pre-filled from resume job titles + employers + dates.
   - Skills tags pre-filled as checkboxes (Q6).
   - Any gap >6 months auto-flagged as "Want help explaining this time?" (invites — does not demand — disclosure).
   - Licenses / certifications extracted for Q7.
4. User still walks the intake — resume accelerates, does not replace.
5. Generated guide cross-references resume: job ideas prioritize occupations where the user already has 50%+ skill overlap per Lightcast skill taxonomy.

**Technical approach (Track A compliant):**
- PDF parsing: `pdf.js` (MIT, in-browser) — no server round-trip.
- DOCX parsing: `mammoth.js` (BSD, in-browser).
- Field extraction: heuristic regex + named-entity pass (compromise.js BSD or a small on-device ML model later).
- Skill matching: fetch Lightcast skills taxonomy JSON (licensable-tier data; must load through **D-2 Path B aggregate adapter** — no raw Lightcast to client. Fetch pre-processed skill-keyword list at build time instead).
- Ashley's persona exposes the critical edge case: a revoked license on the resume must **not** be treated as a current credential. Flag + coach: *"The resume shows X — is that still current?"*

**Privacy:** Mandatory on the upload step: *"Your resume never leaves this device. We parse it in your browser."* Honor the zero-server-PII posture of the Re-Entry web app spec (Component 04).

**Effort:** ~7–10 days end-to-end, including the Ashley-style license-revocation edge case and the skill-matching quality bar.

**Downstream benefit:** The resume becomes the bridge to the **Pathway Explorer** tool next door in WRN. Resume-parsed user → "Here are three occupations where your skills match 60%+" → click through to Pathway Explorer → see wages + career ladder. That's a Component 12 *Alex Suite Integration* win without a new component.

---

## 7. Other tools / resources to build in (from research + adjacent stack)

Surfaced by the research survey (research 01 §5, 02 §6, 03 §§2, 7). Not all are new tools — some are integrations or content fields already possible with existing data.

### T-1. Federal Bonding Program card (P0 — trivial)
$5K free bond, first 6 months, bonds4jobs.com. **Highest-leverage disclosure support we can surface.** A bonded employee is materially easier to hire. One card in the resources section + one mention in the guide's "things you can tell an employer" block.

### T-2. WOTC (Work Opportunity Tax Credit) employer-facing flyer (P1)
Up to $2,400/hire for employers hiring justice-involved workers. **Not disclosed to the jobseeker for their own disclosure** — instead, a printable one-pager the user can hand to a hiring manager. Converts the user into a pitch person for themselves. Authorization status flag needed (authorized through Dec 31, 2025 — confirm for 2026 renewal).

### T-3. NICCC collateral-consequences lookup (P1)
The National Inventory of Collateral Consequences (~44K entries; ~60% employment-related) is a free API. Before the tool recommends any occupation, query NICCC for license restrictions in Indiana. Prevents the Ashley home-health-aide edge case from recurring at scale.

### T-4. Indiana expungement eligibility flag (P1 — information-only, NOT advice)
IC 35-38-9 §5 — misdemeanor eligibility 5 years after conviction, minor felony 8 years, major felony 8–10 years (one-lifetime petition, §8(i)). After expungement, applicants may answer "no" to expunged records (§10(c)). The tool surfaces: *"You may be eligible to petition for expungement — here's who to ask."* Hands off to Indiana Legal Services / Neighborhood Christian Legal Clinic. Never diagnoses eligibility itself (UPL floor).

### T-5. Hamilton County Community Corrections direct-hire pathway card (P0)
HCCC serves 2K+ participants/yr. Mike's relationship + the SOW / HIRE / Recovery Works stack = a named warm-handoff path. Add an "I'm in Community Corrections — connect me to staff" card that emails a pre-filled note to HCCC workforce coordinator (through John / Microsoft Graph if we wire it; mailto: otherwise for v1).

### T-6. Peer mentor request card (P1)
Second Chance Business Coalition has 50+ employers. Homeboy, Delancey, CEO all staff graduates as peer mentors. IHC doesn't have its own peer network yet — but a card that says *"Want to talk to someone who's been where you are?"* + a mailto to Aspire Indiana Health's peer-support line is the placeholder until we do.

### T-7. Printable pocket card with the 30-second answer (P0 — trivial)
Wallet-sized PDF of the user's final Acknowledge → Accountability → Forward pivot answer. Something physical to practice from. Evidence: CEO transitional-jobs model embeds rehearsal as a core practice (Redcross 2012 MDRC).

### T-8. Mock interview audio drill (P2)
Web Speech API asks the question aloud; user records an answer; playback + text transcript for self-review. No scoring (CC-9). Pure rehearsal scaffold. Pairs with G-7.

### T-9. DOL Registered Apprenticeship on-ramp search (P1)
For users without a BA, earning-while-learning apprenticeships are the strongest wage path. API: `apprenticeship.gov`. Filter by Indiana + SOC from the user's story. Visible in the Job Ideas section.

### T-10. Background-check-preview walkthrough (P1 — information-only)
FCRA §1681c(a)(2) — arrest records >7 years old should not appear on most background checks. Many users don't know this. A non-advice explainer + link to free self-pulled reports (Annual Credit Report equivalents for criminal records don't exist federally; state-by-state variance in Indiana). Coaches the user to request their own Indiana State Police background check before interviews so they know what the employer will see.

### T-11. Alex Workforce Ecosystem deep-link from Job Ideas (P0)
Every job idea the tool produces should deep-link to `alex-site-intelligence.html?soc={SOC}` → Workforce tab modal with wage curve, outbound pathway, inbound feeders. **No new build.** Just URL construction. The tool becomes an on-ramp to Alex's proprietary labor intelligence.

### T-12. Soft handoff to Pathway Explorer tool (P0)
Resume-parsed or intake-output users get: *"Want to see where this job could take you?"* → opens Pathway Explorer at `?soc={SOC}`. Zero build. High flywheel value.

### T-13. Second Chance Business Coalition employer finder (P2)
The Coalition publishes member lists (JPMC, Walmart, McDonald's, Microsoft, Eaton). Filter to Indiana locations. The tool names specific employers: *"These companies in your area have publicly committed to hiring people with records."* Massive confidence gain.

### T-14. Indiana CDPA data-minimization posture language (P0 — compliance)
IC 24-15, effective Jan 1, 2026. The privacy panel must state: (a) what data is collected (nothing beyond device storage unless user affirmatively opts in), (b) opt-out path (just close the tab — no account exists), (c) minimization duty (no tracking, no cookies, no analytics PII). Honors D-10 privacy floor.

### T-15. Facilitator dashboard for case managers (Component 10, already specced) (P1)
The jail / Community Corrections / recovery facilitator needs a view to review intake drafts, catch mandatory-report triggers, and coach. Already scoped in `10-case-manager-dashboard/`. Unblocks v2.

---

## 8. Gap backlog (severity-ranked)

| ID | Title | Mike's ask? | Research anchor | Effort | Priority |
|----|-------|:-----------:|-----------------|:------:|:--------:|
| G-1 | Peer-voice sample answers on hard questions | ✅ | Maruna 2001 | 2d+1h | **P0** |
| G-2 | Draft-reflect-revise cycle | ✅ | Maruna; Lundahl 2010 | 3d | **P0** |
| G-4 | Persistent no-penalty skip | ✅ | Elliott 2005; 45 CFR C | <1d | **P0** |
| G-9 | Resume ingest | ✅ | Mike direct | 7–10d | **P0** |
| T-1 | Federal Bonding Program card | | DOL; research 02 §6 | <1d | **P0** |
| T-5 | HCCC direct-hire handoff | | research 01 §5 | 1d | **P0** |
| T-7 | Printable pocket card | | Redcross 2012 | 1d | **P0** |
| T-11 | Alex Workforce deep-link | | existing Alex tool | <1d | **P0** |
| T-12 | Pathway Explorer soft handoff | | existing WRN tool | <1d | **P0** |
| T-14 | CDPA minimization copy | | IC 24-15 | <1d | **P0** |
| G-3 | Stage-of-change gate | | Prochaska/DiClemente | 2d | P1 |
| G-6 | Voice-note input | | research 01 §1.3 | 3d | P1 |
| G-8 | "Help me start" sentence stems | | MI technique | 2d | P1 |
| T-2 | WOTC employer flyer | | DOL / research 02 §6 | 1d | P1 |
| T-3 | NICCC collateral-consequences lookup | | research 02 §6; research 03 §4.2 | 3d | P1 |
| T-4 | Indiana expungement flag | | IC 35-38-9 | 1d | P1 |
| T-6 | Peer mentor request | | research 02 §§1, 6 | 1d | P1 |
| T-9 | Apprenticeship.gov on-ramp | | DOL | 2d | P1 |
| T-10 | Background-check preview | | FCRA §1681c | 2d | P1 |
| T-15 | Facilitator dashboard | | Component 10 | (pre-specced) | P1 |
| G-5 | Mid-intake affirmation | | Miller & Rollnick 2013 | <1d | P2 |
| G-7 | Read-aloud audio | | Doak & Doak 1996 | 1d | P2 |
| T-8 | Mock interview audio drill | | CEO Redcross 2012 | 3d | P2 |
| T-13 | Second Chance Coalition finder | | research 02 §6 | 2d | P2 |

**P0 total effort:** ~20 person-days. Doable as a single 4-week v2 sprint.

---

## 9. Recommended v2 sprint plan (4 weeks)

- **Week 1:** G-1 (peer samples), G-4 (skip discipline), T-1 + T-5 + T-7 + T-11 + T-12 + T-14 (all the low-effort / high-leverage integrations). Ship at end of week as v2 beta.
- **Week 2:** G-2 (reflect-revise cycle) + G-9 phase 1 (resume paste-text path with field extraction, no file upload yet).
- **Week 3:** G-9 phase 2 (file upload: PDF + DOCX + license-revocation edge case).
- **Week 4:** G-3 (stage-of-change gate) + CC-2/CC-5/CC-8/CC-10 regression pass across all three personas. Ship v2.

v3 candidates (P1 tier) slot into the following sprint.

---

## 10. What this document is not

- **Not** a substitute for real user testing with justice-involved and recovery populations. Three personas are a floor, not a ceiling. Once the HCCC / Aspire / MHA partnership path is live, the tool needs IRB-informed user research (research 03 §6.2 — 45 CFR Subpart C).
- **Not** a compliance certification. Component 06 (outside counsel review) still owed. Ashley's ADA-protected recovery framing and Dave's trauma profile both need legal sign-off on the language the tool produces before public release beyond beta.
- **Not** an endorsement of any specific AI scoring approach. Current tool is rules-based on purpose (research 03 §6.1). If AI inference is added later, Obermeyer 2019 / ProPublica *Machine Bias* adversarial testing is a non-optional precondition.

---

*Questions or additions to this test prompt: file against `hamilton-implementation/programs/re-entry-workforce/research/` or push directly to this file.*
