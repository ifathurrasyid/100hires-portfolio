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

* **Native Extraction vs. Third-Party APIs:** I intentionally chose a native Python implementation over third-party SaaS wrappers (e.g., Supadata). This decision was driven by a requirement for **system independence**—ensuring the pipeline remains functional without external API key dependencies, usage quotas, or third-party service costs.
* **Resilient Extraction Logic (YouTube):** Initially built a native Python implementation using `youtube-transcript-api`. When encountering aggressive IP rate-limiting on a corporate network, I pivoted to a **yt-dlp based pipeline**. This bypassed network-level blocks while successfully extracting enhanced metadata (Titles + Upload Dates) that standard APIs often restrict.
* **Portable Engineering:** Designed the scripts with **dynamic relative pathing** using `os.path.abspath`. This ensures the pipeline remains fully functional across different environments (e.g., Office vs. Home setups) without requiring manual configuration of absolute directory paths.
* **Workflow Environment:** Used **Jupyter Notebooks (.ipynb)** within VS Code for state management. This allows for fetching data once and keeping it in memory to prevent unnecessary backend pings while fine-tuning transformation logic.

---

## Challenges & Engineering Solutions

Building this pipeline required navigating several "real-world" infrastructure constraints:

1. **The 429 Rate-Limit Barrier:**
   * **Issue:** Initial extraction attempts were flagged and blocked by corporate network security/YouTube rate-limits.
   * **Solution:** Pivoted to a `yt-dlp` backend. This provided a more robust header-emulation layer that bypassed IP blocks while allowing for high-speed metadata extraction.

2. **Environment Portability (Office vs. Home):**
   * **Issue:** Absolute file paths created breaking changes when switching between different workstations.
   * **Solution:** Refactored the project to use **Dynamic Relative Pathing**. The system self-corrects its directory mapping regardless of the host machine's folder structure.

3. **Metadata Fragmentation:**
   * **Issue:** Standard transcript libraries often return raw text without context (Title/Date), making the research database difficult to audit.
   * **Solution:** Engineered a "Single-Pass Extraction" that bundles transcript content with verified metadata (Titles and Upload Dates) directly into the Markdown headers.

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