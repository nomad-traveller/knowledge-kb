# **AGENTS.md — Knowledge Base Schema & Agent Rules**

---

This document is the **schema layer** of the LLM-wiki pattern. It dictates how an LLM or automated agent ingests published sources, processes quick thoughts/inbox notes, executes queries, and maintains the knowledge base to ensure long-term consistency and OKF v0.2 conformance.

## **1\. Format: OKF v0.2 Specification**

Every wiki page represents an OKF concept formatted as a UTF-8 Markdown file with a YAML frontmatter block delimited by \---. The only strictly required frontmatter field is type.

### **Required and Standard Frontmatter Keys**

| Key | Type / Allowed Values | Description   |
| :---- | :---- | :---- |
| type | Concept | Entity | Source Summary | Analysis | Reference | Playbook | Mandatory identifier for the category of the knowledge artifact. |
| title | String | Human-readable display title. |
| description | String | Concise, one-sentence summary of the page content. |
| tags | List of Strings | Categorization tags (e.g., \[idea, draft, book\]). |
| status | draft | stable | deprecated | Lifecycle state of the document (default is stable). |
| generated | { by: \<actor\>, at: \<ISO8601Z\> } | Provenance detailing who created/updated the file and when. |
| verified | List of { by: \<actor\>, at: \<ISO8601Z\> } | Confirmation events. Prefix human reviews with human:\<id\>. |
| stale\_after | ISO-8601 Instant | Expiration timestamp after which content is deemed stale. |
| sources | List of Source Objects | Attributed sources containing id, resource, and title. |

### **Actor Conventions & Reserved Files**

* **Actor Naming:** human:\<id\> (for humans), \<agent\>/\<version\> (for AI agents), process:\<id\> (for automated scripts).  
* **Per-Claim Attribution:** Use standard Markdown inline footnotes (\[^source-id\]) mapped directly to a sources\[\].id.  
* **Reserved Filenames:** Never use index.md or log.md as concept filenames.

## **2\. Directory Structure**

| Directory Path | Purpose & Access Permissions   |
| :---- | :---- |
| raw/ | **Immutable Sources:** Published papers, PDFs, web clips. (Read-Only) |
| raw/inbox/ | **Inbox & Brain Dumps:** Unstructured quick thoughts, voice transcripts, raw notes. No YAML required. |
| raw/inbox/processed/ | **Inbox Archive:** Storage area for raw notes that have been refactored into the wiki. |
| templates/ | **Mandatory Skeletons:** Reference templates (concept.md, source.md, analysis.md, entity.md). |
| wiki/index.md | **Content Catalog:** Central catalog generated via python3 tools/okf.py rebuild-index. |
| wiki/log.md | **Audit Log:** Chronological history of all changes, newest first. |
| wiki/concepts/ | Structured ideas, patterns, methods, thoughts, and book ideas. |
| wiki/sources/ | Summaries of ingested sources from raw/. |
| wiki/entities/ | Pages for individuals, organizations, and software tools. |
| wiki/analyses/ | Detailed syntheses, comparisons, and chapter drafts. |

## **3\. Operational Workflows**

### **A. Ingest Published Sources**

1. **Deduplicate First:** Consult wiki/index.md to check if a page already exists. If present, extend it rather than creating a duplicate.  
2. **Read Source:** Read the target file in raw/.  
3. **Create Source Summary:** Copy templates/source.md to wiki/sources/\<slug\>.md and fill in provenance metadata.  
4. **Update Knowledge Graph:** Update related entities, concepts, and analyses; insert bundle-relative cross-links (e.g., /concepts/my-concept.md).  
5. **Rebuild & Log:** Rebuild the index (python3 tools/okf.py rebuild-index) and log the change in wiki/log.md.

### **B. Process Inbox & Quick Thoughts (raw/inbox/)**

1. **Scan Inbox:** Read new notes, voice transcripts, or brain dumps in raw/inbox/.  
2. **Extract Ideas:** Identify actionable insights, hypotheses, or chapter ideas.  
3. **Create/Update Concept Pages:** Create a new file in wiki/concepts/ using templates/concept.md (set status: draft and generated.by: human:\<id\> or current agent) or extend existing pages.  
4. **Archive Raw Note:** Move the processed note to raw/inbox/processed/.  
5. **Rebuild & Log:** Update wiki/index.md and append an entry to wiki/log.md.

### **C. Update Pages (Amend vs. Supersede)**

* **Amend:** Edit existing content, add claims with source citations, update generated.at. Use when information is correct but incomplete.  
* **Supersede:** If content is fundamentally flawed or restructured, mark the old page as status: deprecated, set superseded\_by: \<new-path\>, and create a new page. Never delete pages with inbound links.

### **D. Querying & Synthesis**

1. Read wiki/index.md first to identify relevant pages.  
2. Synthesize the response using proper citations. If the synthesis provides durable value, save it as a new page in wiki/analyses/ using templates/analysis.md.

## **4\. Health Checks & Quality Constraints**

### **Linter Validation Checks (python3 tools/okf.py lint)**

* Missing type field in YAML frontmatter.  
* Orphan pages lacking inbound cross-links.  
* Broken internal relative or bundle-relative Markdown links.  
* Stale concepts where now \>= stale\_after.  
* Missing or undersized \#\# Summary sections (\< 40 characters).  
* Page length exceeding 300 lines (requires splitting).  
* Invalid filenames (must use kebab-case ASCII slugs without spaces, dates, or uppercase characters).

### **Log Entry Format (wiki/log.md)**

Log entries must follow a strict, single-line pipe-separated format (newest first):

YYYY-MM-DD | ACTION | path | free-text note

* **Allowed Actions:** create | update | deprecate | delete | ingest | rebuild | maintenance  
* **Example:** 2026-09-02 | create | wiki/concepts/inbox-workflow.md | Added inbox processing pattern

### **Hard Anti-Hallucination & Writing Rules**

* **Strict Provenance:** Never cite a source that is not listed in raw/ or in the page's sources\[\] block. Unverified statements must be marked with *(unverified)*.  
* **Unsure \= Draft:** Any page containing unverified claims must remain in status: draft.  
* **Head-First Rule:** Every document body MUST begin with a \#\# Summary section containing a single self-contained paragraph.  
* **Record Contradictions:** Conflicting sources must be explicitly documented rather than averaged or obscured.