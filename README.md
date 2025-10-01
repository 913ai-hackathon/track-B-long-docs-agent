# Track B — Long Document Processing (100–300 Pages)

## Problem
Enterprises deal with lengthy documents—manuals, policies, reports, and “continuous” evidence packs (e.g., claims or case files)—that agents must process without losing context or accuracy. Think **Cursor for documents**: the agent should navigate, cite, and reason over the entire bundle reliably, including text **and images embedded in PDFs**.

## Core Deliverable
Build an **agent (using OpenAI’s Agents SDK)** that:
1. Processes long documents end-to-end **without exceeding context limits**.
2. Produces **evidence-grounded summaries** with source references.
3. Extracts **structured key facts** across the document.
4. Provides **Q&A** with **page-linked citations**.
5. **Persists** intermediate document information somewhere (e.g., a real-time database) so it can **retrieve and reuse** it later.
6. **(Next level)** Understands **images** inside PDFs (e.g., photos, scans, charts, tables, stamps) and incorporates those findings into answers and summaries with citations back to the exact **image region/page**.

## Example Task
Given a **200-page product manual** and a **150-page policy handbook** (with some scanned/image pages), create a “document workspace” that:
- Stores extracted sections/tables/entities/images in a **persistent store**,
- Answers multi-step questions that require jumping across **text + images**,
- Generates a one-page **executive brief** with **clickable citations** (page/paragraph or image region), and
- Supports follow-up queries later that **reuse** previously stored information without reprocessing the entire files.

## Constraints
- No “dump everything into a single prompt.”
- Must handle mixed content: prose, **tables**, appendices, **embedded images/charts/scans**.
- Outputs must be fully **traceable** to the source (page/section/paragraph or image region anchors).
- **How** you retrieve is up to you (agentic retrieval, rules/metadata, keyword search, structured stores, lightweight vectors, or a mix).
- If using a database, demonstrate **updates** (add/replace a document) without rerunning the entire pipeline.
- Treat vector databases as **optional**; do not rely on them where it harms reliability—**accuracy is paramount**.

## Success Criteria
- **Accuracy first:** Correct summaries and fact extractions; image-derived facts must match what’s visibly present.
- **Coverage:** Major sections **and relevant images** are reflected; provide a coverage report.
- **Efficiency:** Time/resource usage scaled for 100–300 pages; show token and latency budgeting.
- **Evidence:** Every claim includes a resolving citation to the page/section or **image region**.
- **Reliability:** Consistent results across runs and after small corpus updates.
- **Reusability:** Subsequent queries benefit from persisted information (reduced latency/cost demonstrated).
- **Safety & auditability:** Clear provenance logs; easy to audit which sources (text or image) informed each conclusion.

## Stretch Goals
- “What changed” reports between two document versions (section-level + image diffs if relevant).
- Table/Chart extraction from images (figure-to-JSON) with unit/type inference.
- Cross-document reasoning (e.g., reconcile a text policy with a photographed invoice page).
- Interactive outline/mini-map that includes image thumbnails linked to their citations.

---

## Getting Started (Agents SDK)
Use the OpenAI **Agents SDK** for orchestration; pair it with the **Responses API** to call tools and maintain state.

- **Agents SDK (Python) docs:** https://openai.github.io/openai-agents-python/  [oai_citation:5‡OpenAI GitHub](https://openai.github.io/openai-agents-python/?utm_source=chatgpt.com)  
- **Quickstart:** https://openai.github.io/openai-agents-python/quickstart/  [oai_citation:6‡OpenAI GitHub](https://openai.github.io/openai-agents-python/quickstart/?utm_source=chatgpt.com)  
- **Agents guide (platform docs):** https://platform.openai.com/docs/guides/agents-sdk  [oai_citation:7‡OpenAI Platform](https://platform.openai.com/docs/guides/agents-sdk?utm_source=chatgpt.com)  
- **Responses API reference:** https://platform.openai.com/docs/api-reference/responses  [oai_citation:8‡OpenAI Platform](https://platform.openai.com/docs/api-reference/responses?utm_source=chatgpt.com)

### Local setup
```bash
python -m venv .venv
source .venv/bin/activate
pip install openai-agents  # Agents SDK
