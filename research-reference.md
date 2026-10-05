# GiveWell Research Reference

The shape of GiveWell research, the documents it produces, and the research skills this repo reaches through the givewell-research-skills plugin. Written October 2026 as seed context; correct it as you see the work up close.

You're not carrying research yourself — this file exists because the artifacts your grants produce each have a shape and a standard, and knowing what a good one looks like is what makes the PM work legible. It's deliberately general; the Water-specific half (the pod, the PM work, where AI helps in it) lives in `water-pm-reference.md`.

## The work

GiveWell research moves from "is this worth looking at" to "should we fund it," and each step has a recognizable artifact:

- **Quick Evidence Assessments (QEAs)** — a fast, scored read on how strong the evidence base for an intervention is, and what it would take to get to a confident view. The `qea` skill writes and scores these against the rubric senior researchers grade on.
- **BOTECs and CEAs** — back-of-the-envelope and then full cost-effectiveness models, in Google Sheets, reported as a multiple of GiveWell's benchmark. The `botec` skill builds these in GiveWell's template. The polished CEAs the grantmaking pods maintain are where most of the numerical reasoning lives.
- **Literature reviews** — the academic and grey-literature evidence on a question, pulled together and synthesized. The `lit-review` skill does the retrieval and a first synthesis.
- **Intervention reports and investigation memos** — the deeper write-ups an area gets if it survives the early cuts: what was found, how confident the researcher is, what would change their mind.
- **Investigation plans (IPs), conditional approvals (CAs), and grant pages** — the plan for an investigation, the internal recommendation document, and the published version of it. These are the artifacts every grant you shepherd produces: the CA is where the pod's recommendation lives, and the CA-to-published-page path is what turns internal work into public commitment. Grant pages are what donors actually read; Research Ops maintains the CA template and runs the CA-to-published-page pipeline.
- **Peer review and vetting** — GiveWell checks its own work before it goes out. Vetting traces the numbers in a workbook; peer review argues with the reasoning. Commons runs the vetting; an AI peer-review layer is being built alongside it.
- **Lookbacks** — the retrospective read on a past grant or analysis: what happened, and what the original work got wrong.

Published, finished versions of most of this are public at [givewell.org/research](https://www.givewell.org/research). Reading a few is the fastest way to see the standard — the water quality pages (chlorination and the grant pages for in-line chlorination and Dispensers for Safe Water) are the closest to your pod's grants.

## The research skills you have

They come from the **givewell-research-skills** plugin — the same live versions the research team uses, installed via the pointer in `.claude/settings.json` rather than copied here, so they stay current without anyone syncing files. You won't run most of them daily, but they're the fastest way to understand the artifacts your grants produce, and useful when a piece of research support lands on you:

1. **lit-review** — find and synthesize the evidence on a topic; a Python retrieval layer over OpenAlex, Semantic Scholar, PubMed, and Crossref with an AI synthesis on top, plus a built-in review mode that checks coverage and that every citation is real.
2. **research-radar** — scan for new academic and grey-literature research on the programs GiveWell funds or might fund, tagged with why each item matters to GiveWell.
3. **qea** — write or score a Quick Evidence Assessment to the senior-researcher grading standard.
4. **botec** — build a GiveWell-style BOTEC (one tab per program, conformed to the mortality-CEA and VoI templates), with a cost-effectiveness multiple as the headline.
5. **peer-review** — run a peer review on a research memo or report, with citation verification.
6. **givewell-footnotes** — turn factual claims into verified footnotes with direct source quotes. Of the research skills, the one most likely to touch publishing work directly.
7. **data-analysis** — structured data work: pulling, reconciling, and analysing datasets with the checks written down.
8. **verify** — check a draft's claims against the sources it cites before it goes out.
9. **legibility-review** — check a draft against GiveWell's legibility standards (bottom line first, named uncertainty, real opinions).
10. **submit-feedback** — file a bug, rough edge, or skill idea about any of the above.

The GiveWell standards these run against — the QEA rubric and templates, the BOTEC templates, moral weights, the style guide, the legibility guidance, and `environments.md` — ship in the plugin's `reference/` folder (on a machine that has added the marketplace: `~/.claude/plugins/marketplaces/givewell-research-skills/plugin/reference/`). A short summary of the legibility standards also lives in `guidelines/legibility-guidance.md` here.

## Where AI helps and where it fails

The PM-specific version of this lives in `water-pm-reference.md`. The short version for research artifacts: AI is strong at recomputing numbers, tracing structure, applying explicit rules, and first-draft synthesis — and it fails by hallucinating citations, omitting silently (dropped tables, truncated output that looks complete), missing comments and out-of-document context, and being wrong with full confidence. Never accept an AI-verified citation without opening the source; that's what the verification layers in `lit-review` and `givewell-footnotes` exist for.
