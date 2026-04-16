# 100Hires Portfolio: Cold Outreach Research Pipeline

## Project Overview
This repository serves as a technical portfolio and research hub for the 100Hires application process. The core objective is building a resilient data pipeline to aggregate high-signal insights on **B2B SaaS Cold Outreach** from top industry practitioners. This structured data repository is designed to eventually be fed into an LLM or used to construct a step-by-step outbound playbook.

---

## The "Why": Expert Selection Methodology

When curating the data sources, I deliberately bypassed generic "sales influencers." I focused strictly on **tactical practitioners** who treat the outbound pipeline as a quantifiable, technical system.

The chosen 10 experts specialize in:
* **A/B Testing & Data Benchmarks:** (e.g., Will Allred, Florin Tatulea)
* **Intent-Signal & TAM Analysis:** (e.g., Eric Nowoslawski, Jed Mahrle)
* **Systematic Personalization & Triggers:** (e.g., Becc Holland, Charlotte Johnson)
* **Workflow & Sequence Architecture:** (e.g., Jason Bay, Josh Braun)
* **Execution & Deal Logic:** (e.g., John Barrows, Armand Farrokh)

---

## Technical Architecture & Decision Logic

I prioritized system resilience and scalability, adapting to roadblocks dynamically:

* **Resilient Extraction Logic (YouTube):** Initially built a native Python implementation. When encountering aggressive IP rate-limiting on a corporate network, I pivoted to a **yt-dlp based pipeline**. This bypassed network-level blocks while successfully extracting enhanced metadata (Titles + Upload Dates) that standard APIs often restrict.
* **Portable Engineering:** Designed the scripts with **dynamic relative pathing** using `os.path.abspath`. This ensures the pipeline remains fully functional across different environments (e.g., Office vs. Home setups) without requiring manual configuration of absolute directory paths.
* **"Smart Manual" Extraction (LinkedIn):** Designed a targeted extraction process to safely capture high-value posts without triggering anti-bot protocols, ensuring data integrity for the master source list.
* **Workflow Environment:** Used **Jupyter Notebooks (.ipynb)** within VS Code for state management. This allows for fetching data once and keeping it in memory to prevent unnecessary backend pings while fine-tuning transformation logic.

---

## Challenges & Engineering Solutions

Building this pipeline required navigating several "real-world" infrastructure constraints:

1. **The 429 Rate-Limit Barrier:** * **Issue:** The initial Python implementation using `youtube-transcript-api` was flagged and blocked by corporate network security/YouTube rate-limits.
   * **Solution:** Pivoted to a `yt-dlp` backend. This provided a more robust header-emulation layer that bypassed the IP blocks while allowing for high-speed metadata extraction.

2. **Environment Portability (Office vs. Home):**
   * **Issue:** Absolute file paths created breaking changes when switching between different workstations.
   * **Solution:** Refactored the entire project to use **Dynamic Relative Pathing** via `os.path.abspath`. The system now self-corrects its directory mapping regardless of the host machine's folder structure.

3. **Metadata Fragmentation:**
   * **Issue:** Standard transcript libraries often return raw text without context (Title/Date), making the research database difficult to audit.
   * **Solution:** Engineered the V2 pipeline to perform a "Single-Pass Extraction" that bundles the transcript content with verified metadata (Titles and Upload Dates) directly into the Markdown headers.

---

## Current Progress

### Phase 1: Environment Setup (Completed)
- [x] Configured IDE and AI tooling.
- [x] Established GitHub version control and remote repository.
- [x] Resolved corporate network restrictions via library pivoting.

### Phase 2: Research & Extraction (Completed)
- [x] **Expert Selection:** Curated 10 practitioners focused on systems-based outreach, documented in `research/sources.md`.
- [x] **YouTube ETL Pipeline:** Automated extraction of transcripts and metadata, saved as standardized Markdown.
- [x] **LinkedIn Pipeline:** Safely extracted 10 tactical posts directly from the selected experts.

---

## Repository Structure

```text
100hires-portfolio/
├── scripts/
│   └── youtube_etl.ipynb      # Robust yt-dlp extraction logic (Portable/Resilient)
├── research/
│   ├── sources.md             # Master index (10 experts, dates, & annotations)
│   ├── youtube-transcripts/   # 10 formatted Markdown transcripts 
│   └── linkedin-posts/        # 10 raw text Markdown files of high-value posts
└── README.md