# SME Feedback: Incident Response and Postmortems
**Module:** Week 3, Class 6 — Incident Response and Postmortems  
**Reviewer:** Sumit Rahman  
**Documents Reviewed:** README.md (student-facing), Instructor Guide

---

## Overall Assessment

This is the strongest lesson in Unit 2 so far. The conceptual content is tight, the framing is accurate, and the "silent failure" thread running from the learning objectives
through the Rogue Pricing Algorithm example to the postmortem design section is the kind of coherent narrative that distinguishes good adult education. The Five Whys
example is grounded, the blameless vs. blame-focused action item contrast is memorable, and the Tooling Context section (Docker + GitHub) is a rare case of a lesson correctly
explaining *why* a tool is used rather than just naming it.

The primary gap remains the same production blocker that has appeared in every prior module: the lab section defers to an unspecified external resource. The lab materials
produced alongside this feedback are self-contained and resolve this.

---

## 1. Structural Issues

**Issue 1.1 — Incident Response Lifecycle: Five Stages Listed, Six in the Diagram**

Section 1 lists five stages in prose (Preparation, Identification, Containment,
Remediation & Recovery, Lessons Learned) but the Mermaid diagram shows six nodes,
splitting "Remediation & Recovery" into separate "Remediation" and "Recovery" nodes.
This inconsistency will confuse students during the debrief — one of the reflection
questions asks them to trace failures through the lifecycle, and the two counts do not
match. The prose and the diagram should use the same taxonomy. The six-stage diagram is
more accurate for production practice; the prose should be updated to match.

**Issue 1.2 — Lab Section Defers to External Repository (Production Blocker)**

Section 5 states: *"Please refer to the dedicated Lab Guide for the mock incident
scenario details, timeline logs, and the postmortem document template."* No repository
URL, path, or file name is provided. This is the fifth consecutive module with this
issue. The lab materials provided alongside this feedback are self-contained.

**Issue 1.3 — Section 4 "Tooling Context" Not Reflected in Table of Contents Timing**

The Session Breakdown table allocates 60 minutes to the lab and 20 minutes each to
Sections 1–3 (total: 120 minutes). However, Section 4 (Tooling Context) is not listed
in the Session Breakdown at all, meaning either it is covered within the 20-minute
Section 3 slot or it was added to the README after the timing was set. The instructor
guide correctly combines Sections 3 and 4 into a single 25-minute "Blameless
Postmortems & Tooling" segment. The student-facing README should reflect this same
structure.

---

## 2. Alignment with Syllabus and Competency Map

| Learning Objective | In README? | In Instructor Guide? | Notes |
|---|---|---|---|
| Outline the stages of effective incident response | ✅ Section 1 | ✅ Yes | Minor inconsistency in stage count (5 vs 6) — see Issue 1.1 |
| Apply structured approaches to document and analyse incidents | ✅ Section 2 | ✅ Yes | Five Whys example is well chosen |
| Design blameless postmortems with systemic action items | ✅ Section 3 | ✅ Yes | Contrast of bad vs. good action items is the clearest single teaching moment in Unit 2 |

All three LOs are fully addressed in both documents.

---

## 3. Technical Content

**Issue 3.1 — "Silent Failure" Defined Too Narrowly**

Section 1 correctly identifies the silent failure concept but defines it only as "data
drift or biased predictions." The module's own Rogue Pricing Algorithm example is also
a silent failure (the API returns 200 OK, prices are just wrong). The definition should
be broadened: a silent failure is any condition where the infrastructure is healthy but
the system is not performing its intended function correctly — including stale features,
model version mismatches, and feature encoding errors, not just drift.

**Issue 3.2 — No Mention of Incident Severity Tiers (P1–P4)**

The instructor guide references severity tiers implicitly (the Rogue Pricing example is
clearly P1-equivalent) but neither document defines or uses severity levels. In
practice, severity classification is the first decision an incident commander makes —
it determines escalation, response time, and communication cadence. Adding a brief
severity tier definition (P1: total outage or critical data integrity failure; P2: major
degradation; P3: limited impact; P4: monitoring gap) would give students the vocabulary
they need for the postmortem lab.

**Issue 3.3 — "Runbook" Mentioned Once, Not Defined**

Section 1 lists "runbooks" as part of Preparation but does not define what a runbook
is. The instructor guide does not elaborate. Students new to operations may not know
that a runbook is a documented set of procedures for responding to specific failure
modes — exactly what INC-002 lacked. One sentence of definition in Section 1 would
scaffold the action item in Part 4 of the lab that asks students to write a runbook gap
remediation.

---

## 4. Instructor Guide

**Issue 4.1 — Pacing Table Misaligns Segment Names with README Structure**

The instructor pacing table has four rows:
1. "The Stages of Incident Response" — 10 min
2. "Structured Approaches to Analysis" — 25 min
3. "Blameless Postmortems & Tooling" — 25 min
4. "Lab" — 60 min

But the README has four numbered sections (1–3 + Section 4 Tooling Context) before the
lab reference. Segment 3 in the pacing guide covers both README Sections 3 and 4 — this
is reasonable, but it should be made explicit so instructors know that Section 4 is not
a separate time block.

**Issue 4.2 — Common Student Issue: "Jump Straight to Fix" Should Specify the Intervention**

The troubleshooting table correctly identifies that students skip containment and jump
to coding a fix. The suggested instructor intervention — *"Production is still burning.
Your fix will take 30 minutes to build. How do you stop the bleeding right now?"* — is
strong. However, the table does not specify what the correct answer is, leaving
instructors to improvise. The expected answer should be stated: activate the fallback
heuristic model (as referenced in the lesson's own Section 1) and communicate status to
stakeholders before writing a single line of code.

---

## 5. Theory-to-Lab Alignment Recommendations

> *These are forward-looking recommendations, not criticisms.*

**Recommendation 5.1 — Add Severity Tier Vocabulary to Section 1**  
The lab asks students to assign severity to INC-002 (Stretch Problem 5.1). This is
unsupportable without a definition in the lesson. Adding a P1–P4 table to Section 1
would scaffold the stretch problem and is standard SRE vocabulary students will
encounter in every industry role.

**Recommendation 5.2 — Add Feature Freshness SLI Example to Section 1**  
The lab's most important teaching moment is the discovery that INC-002 was invisible to
all existing metrics — the missing observable was feature freshness. Adding a brief
callout in Section 1 or 2 that names "data freshness" and "model input staleness" as
AI-specific SLIs would connect the lecture theory to the lab's analytical conclusion.

**Recommendation 5.3 — Connect Postmortem Action Items to Observability Tooling**  
The instructor guide's second debrief question asks: *"How could you use Prometheus and
Grafana to automatically detect the issue we simulated today?"* This is the right
question but it appears only in the instructor guide debrief. Surfacing it as a lab
problem (which Part 4.2 now does) grounds the abstract debrief in concrete deliverable
format.

---

## Summary of Action Items

| Priority | Issue | Type | Owner |
|---|---|---|---|
| High | Provide lab scenario details, timeline data, and postmortem template — remove external repo reference | Fix | Content Author |
| High | Reconcile incident lifecycle stage count (5 in prose vs. 6 in diagram) | Fix | Content Author |
| Medium | Add Section 4 to Session Breakdown timing table | Fix | Content Author |
| Medium | Broaden "silent failure" definition beyond data drift | Fix | Content Author |
| Medium | Define "runbook" on first use in Section 1 | Fix | Content Author |
| Medium | Add P1–P4 severity tier definitions to Section 1 | Recommendation | Content Author |
| Medium | Specify expected containment answer in instructor troubleshooting table | Fix | Content Author |
| Low | Clarify that pacing Segment 3 covers both README Sections 3 and 4 | Fix | Content Author |
| Low | Add feature freshness / data freshness as AI-specific SLI examples | Recommendation | Content Author |
