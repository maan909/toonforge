# ToonForge

**ToonForge** — convert documents (PDF, DOCX, TXT) into a structured **TOON** format optimized for LLM ingestion, RAG, and programmatic workflows.

> Version: v0.1 — Minimal converter (document → TOON JSON).  
> Purpose of v0.1: provide a small, dependable pipeline that extracts text + light layout info, splits the content into semantic scenes, and outputs a validated TOON JSON that can be used directly as an LLM prompt or system message.

---

## Why ToonForge?

LLMs work far better when documents are provided with semantic structure (headers, paragraphs, captions) and simple layout metadata. ToonForge turns arbitrary documents into a compact, LLM-friendly JSON representation — the **TOON** format — so apps can reliably prompt LLMs with useful, structured context. 

---

## What v0.1 offers

- Read PDF, DOCX, and TXT files.
- Extract text (uses OCR fallback for PDFs if selectable text is absent when configured).
- Detect simple semantic scenes: `header`, `paragraph`, `list_item`, `caption`, `code`.
- Return a `TOON` JSON (pages → scenes → metadata) that is ready to be used as an LLM prompt or system message.
- CLI: `toonforge convert <file> -o out.toon.json`

v0.1 is intentionally minimal and offline-first (no LLM calls). Future versions will add layout reconstruction, table/figure extraction, diffs, and knowledge graph features.

---

## TOON JSON (example)

```json
{
  "version": "0.1.0",
  "source": "samples/report.pdf",
  "meta": {
    "pages": 2
  },
  "pages": [
    {
      "page": 1,
      "scenes": [
        {
          "id": "3c4e...-id",
          "scene_type": "header",
          "text": "Executive Summary",
          "bbox": [20, 30, 560, 80]
        },
        {
          "id": "7a12...-id",
          "scene_type": "paragraph",
          "text": "Revenue increased 24% year-over-year...",
          "bbox": [20, 90, 560, 140]
        }
      ]
    }
  ],
  "graph": {
    "nodes": [],
    "edges": []
  }
}
