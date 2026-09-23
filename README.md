# bpns-workflow-practice

This is exercise 1 from onboarding: running the EMO-BON data pipeline as a **GitHub Action**, automatically, on GitHub's own infrastructure — rather than running it locally (that's exercise 2, see `bpns-workflow-local`).

The pipeline has 4 phases overall:

Google Sheets --> local CSV --> validated CSV --> RDF graph (RO-Crate) --> published web page

This repo runs the **entire pipeline, end to end, unattended**, using the real `observatory-bpns-crate` workflow template.

---

## Step 1: Create the repository

Created a personal repo (`Hamideh-B-H/bpns-workflow-practice`) to practice in, rather than touching the real `observatory-bpns-crate` repo directly. A safe sandbox — anything that breaks only breaks this copy.

## Step 2: Add the observatory's workflow file

Placed `observatory-bpns-crate`'s own `workflow.yml` into this repo, at the exact path GitHub requires:

```
.github/workflows/workflow.yml
```

GitHub Actions only looks for workflow definitions in that folder — anywhere else, the file is simply ignored.

## Step 3: Understand what the file contains

Before changing anything, read through the file's structure:

- **Workflow** — the whole recipe, defined in `workflow.yml`
- **Trigger (`on:`)** — the event that starts it: `schedule` (runs on a timer) and `workflow_dispatch` (a manual "Run workflow" button on GitHub)
- **Jobs** and **steps** — the ordered sequence of tasks inside the workflow
- **Actions** — reusable, pre-built steps: `actions/checkout`, then the chain `populate-action` → `data-quality-control-action` → `semantic-uplifting-action` → `subsetted-distribution-creation-action` → `rocrate-to-pages` → `actions-gh-pages`

## Step 4: Make the three required changes

The template is shared across every observatory repo — only a handful of values needed changing for this copy:

- Changed `DATA_QUALITY_CONTROL_ASSIGNEE` from `isanti` (the real BPNS assignee) to `Hamideh-B-H` — so any auto-generated issue notifies the right person
- Enabled **read/write permissions** for GitHub Actions in the repo settings — by default Actions only get read access, and this workflow needs to write files back (commit results, push to `gh-pages`)
- Set up **GitHub Pages** in the repo settings — this is what turns the final output into a live web page

## Step 5: Commit the file properly

The file didn't actually commit on the first attempt — had to recreate it and choose **"Commit directly to main"** rather than opening a pull request, since this is a solo practice repo and a PR would just sit unreviewed.

## Step 6: Trigger the workflow manually

Used `workflow_dispatch` — the trigger that adds a "Run workflow" button on the Actions tab — to start the pipeline by hand, rather than waiting for its scheduled time.

## Step 7: Verify the full pipeline ran

Three concrete signs of success:

- **Populated data folders** appeared in the repo (raw/filtered/transformed logsheets)
- A new **`gh-pages` branch** was created automatically
- A **live published page** appeared at `https://hamideh-b-h.github.io/bpns-workflow-practice` — the final linked-data output, generated entirely by GitHub's own servers

---

## The core idea

Every observatory repo (BPNS, RFormosa, and the rest) runs the *exact same* `workflow.yml` template — only a handful of values differ (the Google Sheets URLs, the assignee). This exercise proved that template could be taken, adapted for a few observatory-specific values, and get the entire pipeline — download, validate, convert to RDF, publish — running unattended on GitHub's infrastructure.

---

## Progress

- [x] Step 1: repository created
- [x] Step 2: workflow.yml added at the correct path
- [x] Step 3: workflow structure understood
- [x] Step 4: three required changes made
- [x] Step 5: file committed to main
- [x] Step 6: workflow triggered manually
- [x] Step 7: full pipeline verified — published page live

See also: [bpns-workflow-local](https://github.com/Hamideh-B-H/bpns-workflow-local) — the same pipeline run locally, phase by phase, instead of automatically.
