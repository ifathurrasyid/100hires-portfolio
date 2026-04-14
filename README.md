# 100Hires Portfolio: Cold Outreach Research Pipeline

## Project Overview
This repository serves as a technical portfolio and research hub for the 100Hires application process. The current phase focuses on building an automated ETL (Extract, Transform, Load) pipeline to gather high-signal data on **B2B SaaS Cold Outreach** from top industry practitioners.

---

## Technical Architecture & Decision Logic

As a data analyst, I’ve prioritized system resilience and scalability over "quick" solutions. Key architectural choices include:

* **Extraction Method:** Pivoted from third-party APIs (Supadata) to a native Python implementation using `youtube-transcript-api` and `scrapetube`. This removed dependency on API keys and rate limits, allowing for a more stable, production-ready pipeline.
* **Workflow Environment:** Used **Jupyter Notebooks (.ipynb)** within VS Code for the extraction process. This allows for state management (fetching data once and keeping it in memory) to prevent unnecessary pings to YouTube’s backend while fine-tuning the transformation logic.
* **Separation of Concerns:** Organized the repository to separate logic from data.
    * `/scripts/`: Contains the ETL logic and extraction notebooks.
    * `/research/`: Dedicated storage for the final curated data and source documentation.

---

## Current Progress

### Phase 1: Environment Setup (Completed)
- [x] Configured Cursor IDE with Claude Code and Codex.
- [x] Established GitHub version control and remote repository.
- [x] Resolved corporate network restrictions using Cloudflare WARP.

### Phase 2: Research & Extraction (In Progress)
- [x] **Expert Selection:** Curated a list of 10 practitioners focused on systems-based outreach logic (see `research/sources.md`).
- [x] **YouTube ETL Pipeline:** Built an automated script to scan channels, fetch transcripts, and format them into standardized Markdown files.
- [ ] **LinkedIn Pipeline:** Currently designing a "Smart Manual" extraction process to safely capture high-value posts without triggering platform anti-bot protocols.

---

## Repository Structure

```text
100hires-portfolio/
├── scripts/
│   └── youtube_etl.ipynb      # Automated YouTube extraction logic
├── research/
│   ├── sources.md             # Curated list of 10 experts & justifications
│   ├── youtube-transcripts/   # Formatted output from the ETL pipeline
│   └── linkedin-posts/        # (Upcoming) Structured LinkedIn data
└── README.md