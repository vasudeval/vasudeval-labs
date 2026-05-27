# Titan Series — Local AI Data Preprocessing Engines

Six zero-dependency Go CLI tools for LLM data preprocessing. Run locally, no cloud calls, no Python overhead.

Built for developers who need to prepare documents, audio, and text datasets for LLM pipelines without paying per-page SaaS fees or fighting Python memory limits.

**Website:** [vasudeval.com](https://vasudeval.com) | **Licenses:** [Polar](https://vasudeval.com)

---

## Tools at a Glance

| Tool | What it does | Peak RAM | Speed |
|---|---|---|---|
| [Titan-Doc](#titan-doc) | PDF / DOCX / XLSX → clean Markdown | 3.56 MB heap | 75.30 MB/sec |
| [Titan-Ingest](#titan-ingest) | Documents → chunked JSON for vector DBs | < 50 MB | 400+ docs/sec |
| [Titan-Audio](#titan-audio) | Audio / video → Whisper-ready WAV | < 13 MB | 24.6x realtime |
| [Titan-Forge](#titan-forge) | Markdown → PII-scrubbed token chunks | 73.44 MB | 19,112 redactions/sec |
| [Titan-Purge](#titan-purge) | Text datasets → deduplicated corpus | < 22 MB | 128-bit MinHash LSH |
| [Titan-Shield](#titan-shield) | Local DLP proxy for outbound AI API calls | 2.79 MB heap | ~95.50 MB/sec |

All tools:
- Single static binary, no runtime dependencies
- Free trial mode works without a license key (limits noted per tool)
- Licensed via [Polar](https://vasudeval.com) for production use

---

## Download & Run

1. Go to [Releases](https://github.com/vasudeval/vasudeval-labs/releases/latest)
2. Download the zip for your platform and tool
3. Unzip and run

**Linux / macOS:**
```bash
unzip titan-doc-linux-amd64.zip
chmod +x titan-doc
./titan-doc -in ./test_files -out ./output
```

**Windows:**
```powershell
# Unzip titan-doc-windows-amd64.zip, then:
.\titan-doc.exe -in .\test_files -out .\output
```

Replace `titan-doc` with the tool you want: `titan-ingest`, `titan-audio`, `titan-forge`, `titan-purge`, `titan-shield`.

---

## Titan-Doc

**PDF / DOCX / XLSX → clean Markdown**

Extracts text and tables from document files into flat Markdown. Strips recurring headers, footers, and page numbers inline during extraction. Dense spreadsheet tables become standard `|---|---|` Markdown, not broken prose.

Use this before feeding documents into any RAG pipeline or LLM context.

**Demo:** [Watch 181 MB processed in 2.4 seconds](https://youtu.be/noDs2xnzpJM)

### Benchmarks

| Metric | Value |
|---|---|
| Input | 181.06 MB — 23 files (PDFs, DOCX, XLSX) |
| Output | 0.43 MB clean Markdown |
| Duration | 2.40 seconds |
| Throughput | 75.30 MB/sec |
| Peak heap (HeapAlloc) | 3.56 MB |
| Total system RAM | 18.15 MB |

### Quickstart

**Free trial** — processes up to 3 pages or rows per file, no license needed:
```bash
# Linux / macOS
./titan-doc -in ./test_files -out ./markdown_outputs

# Windows
.\titan-doc.exe -in .\test_files -out .\markdown_outputs
```

**Licensed** — unlimited files, recursive directories:
```bash
# Linux / macOS
./titan-doc -in /path/to/source_dir -out /path/to/output -lic "YOUR_KEY"

# Windows
.\titan-doc.exe -in "C:\source_dir" -out "C:\output" -lic "YOUR_KEY"
```

### Flags

| Flag | Description |
|---|---|
| `-in` | Input directory (`.pdf`, `.docx`, `.xlsx`) |
| `-out` | Output directory for `.md` files |
| `-lic` | Polar license key (omit for trial) |

**[Get license →](https://buy.polar.sh/polar_cl_OCEX5FlOytMtbV48UZ2LVUD1vJtPJ01RwTz4t05IVVu)**

---

## Titan-Ingest

**Documents → chunked JSON for vector databases**

Parses PDF, HTML, and text files and splits them into semantic chunks ready for embedding. Splits at natural boundaries — headings, table rows — not fixed character counts. Outputs a single JSON file with chunks, source metadata, and a hash per chunk. Drop it directly into Pinecone, Weaviate, Chroma, or any vector DB ingestion pipeline.

**Demo:** [Watch the 140x performance demo](https://youtu.be/aShsIDnLZRk)

### Benchmarks

| Metric | Value |
|---|---|
| Throughput | 400+ complex technical docs/sec |
| Peak RAM | < 50 MB |
| Concurrency | Lock-free parallel Go worker pool |

### Quickstart

**Free trial** — up to 20 files, 30 pages per file:
```bash
# Linux / macOS
./titan-ingest -in /path/to/documents

# Windows
.\titan-ingest.exe -in "C:\path\to\documents"
```

**Licensed:**
```bash
# Linux / macOS
./titan-ingest -in /path/to/docs -out /path/to/nodes.json -workers 4 -lic "YOUR_KEY"

# Windows
.\titan-ingest.exe -in "C:\docs" -out "C:\nodes.json" -workers 4 -lic "YOUR_KEY"
```

### Flags

| Flag | Description | Default |
|---|---|---|
| `-in` | Input directory (`.pdf`, `.html`, `.txt`) | required |
| `-out` | Output JSON path | `ingested_nodes.json` |
| `-workers` | Parallel workers (licensed only) | 1 |
| `-lic` | Polar license key | — |

**Output structure:** `ingested_nodes.json` — array of chunks, each with content, source file, section heading, and a unique hash.

**[Get license →](https://buy.polar.sh/polar_cl_7JmTYuEIzOK6nHnWrlUt9Q8l2kmT4LOQO6Syd26xemD)**

---

## Titan-Audio

**Audio and video → Whisper-ready WAV**

Converts any mix of `.mp4`, `.mkv`, `.wav`, `.mp3`, `.m4a` files to 16kHz mono 16-bit linear PCM WAV — the exact format Whisper expects. Pipes directly through FFmpeg at the kernel level, so RAM stays flat regardless of how large the input files are. Outputs a JSON manifest with per-file stats: duration, peak dB, sample rate.

**Demo:** [Watch the preprocessing demo](https://youtu.be/PKY7JPWxfLI)

> **Requires FFmpeg on your system.**
> Linux: `apt install ffmpeg` | macOS: `brew install ffmpeg` | Windows: [ffmpeg.org](https://ffmpeg.org/download.html)

### Benchmarks

| Metric | Value |
|---|---|
| Input dataset | 101.35 MB |
| Peak RAM | 12.46 MB (flat) |
| Processing speed | 24.6x realtime |
| Concurrency | Lock-free worker pool |

### Quickstart

**Free trial** — up to 5 files, 10 min per file max:
```bash
# Linux / macOS
./titan-audio -in ./media_dir -out ./whisper_ready

# Windows
.\titan-audio.exe -in "C:\media_dir" -out "C:\whisper_ready"
```

**Licensed:**
```bash
# Linux / macOS
./titan-audio -in ./media_dir -workers 4 -lic "YOUR_KEY"

# Windows
.\titan-audio.exe -in "C:\media_dir" -workers 4 -lic "YOUR_KEY"
```

### Flags

| Flag | Description | Default |
|---|---|---|
| `-in` | Input directory of media files | required |
| `-out` | Output directory for WAV files | required |
| `-workers` | Parallel workers (licensed only) | 1 |
| `-lic` | Polar license key | — |

**Output:** `.wav` files at 16kHz mono 16-bit PCM + `manifest.json` with per-file duration, peak dB, and sample rate.

**[Get license →](https://buy.polar.sh/polar_cl_fjnkoggFxnnlaqSwuhVXHGNk025W1LngmCSOh1yM6N0)**

---

## Titan-Forge

**Markdown / text → PII-scrubbed, token-bounded JSON chunks**

Two-pass stream processor. First pass scrubs emails, IP addresses, and API key patterns via precompiled regex. Second pass splits content into token-bounded chunks with configurable size and overlap, preserving the parent heading for each chunk. Everything runs locally — no data leaves the machine.

Use this before sending any internal documents into an LLM or vector database.

**Demo:** [Watch 100K lines, 40K redactions in 2 seconds](https://youtu.be/ZKgoJdrQJIE)

### Benchmarks

| Metric | Value |
|---|---|
| Input | 100,000 lines with 40,000 injected PII patterns |
| Redactions executed | 40,000 (emails, IPs, API keys) |
| Chunks generated | 4,000 token-bounded blocks |
| Duration | 2.09 seconds |
| Redaction rate | 19,112 redactions/sec |
| Peak RAM | 73.44 MB |

### Quickstart

**Free trial** — 5 files max, 10 chunks per file, watermark appended to output blocks:
```bash
# Linux / macOS
./titan-forge -in ./test_vault -out ./chunks.json -size 500 -overlap 50

# Windows
.\titan-forge.exe -in .\test_vault -out .\chunks.json -size 500 -overlap 50
```

**Licensed:**
```bash
# Linux / macOS
./titan-forge -in /path/to/source -out /path/to/output.json -size 500 -overlap 50 -workers 4 -lic "YOUR_KEY"

# Windows
.\titan-forge.exe -in "C:\source" -out "C:\output.json" -size 500 -overlap 50 -workers 4 -lic "YOUR_KEY"
```

### Flags

| Flag | Description | Default |
|---|---|---|
| `-in` | Input directory (`.md`, `.txt`) | required |
| `-out` | Output JSON file path | required |
| `-size` | Max tokens per chunk | 500 |
| `-overlap` | Token overlap between chunks | 50 |
| `-workers` | Parallel workers (licensed only) | 1 |
| `-lic` | Polar license key | — |

**Output:** `forge_chunks.json` — array of chunks with scrubbed content, token count, parent heading, and source file.

**[Get license →](https://buy.polar.sh/polar_cl_ozDCIe3MbuW1R4MwIOp5cFF9nBCN5VNq48O5K1aRTHB)**

---

## Titan-Purge

**Text dataset deduplication using MinHash LSH**

Computes 128-band MinHash signatures via Murmur3 for every file in a directory, then runs pairwise Jaccard similarity comparison. Flags exact duplicates (100% match) and near-duplicates (≥ 85% similarity) in a JSON manifest. Runs entirely offline with no external dependencies.

Run this before building a vector index or fine-tuning dataset to avoid indexing redundant content.

**Demo:** [Watch the LSH deduplication demo](https://youtu.be/4vsMBnLZ2aw)

### Benchmarks

| Metric | Value |
|---|---|
| Peak RAM | < 22 MB |
| Hash matrix | 128-bit Murmur3 seeds |
| Similarity threshold | ≥ 85% Jaccard |
| Concurrency | Non-blocking parallel worker pool |

### Quickstart

**Free trial** — up to 5 files, no directory recursion:
```bash
# Linux / macOS
./titan-purge -in ./raw_dataset -out ./signatures

# Windows
.\titan-purge.exe -in .\raw_dataset -out .\signatures
```

**Licensed:**
```bash
# Linux / macOS
./titan-purge -in /path/to/dataset -out /path/to/output -workers 4 -lic "YOUR_KEY"

# Windows
.\titan-purge.exe -in "C:\dataset" -out "C:\output" -workers 4 -lic "YOUR_KEY"
```

### Flags

| Flag | Description | Default |
|---|---|---|
| `-in` | Input directory (`.txt`, `.log`, `.json`, `.csv`, `.md`) | required |
| `-out` | Output directory | required |
| `-workers` | Parallel workers (licensed only) | 1 |
| `-lic` | Polar license key | — |

**Output:** `purge_manifest.json` — duplicate pairs with Jaccard scores, flagged as exact or near-duplicate, plus a clean deduplicated file list.

**[Get license →](https://buy.polar.sh/polar_cl_PNYfBKzakuI0ZHPu0LNNUaOmUnBzEMPDU3aAY0KpmaF)**

---

## Titan-Shield

**Local reverse proxy that scrubs sensitive data from outbound AI API calls**

Sits between your application and any LLM API endpoint (OpenAI, Anthropic, etc.). Inspects the outbound JSON payload, applies regex rules against field values, and either redacts matched patterns before forwarding or blocks the request with a 403. All rules and audit logs stay local. Sub-millisecond inspection latency.

Useful when developers are sending internal code, credentials, or customer data to hosted AI endpoints and you need a local enforcement layer without a heavy enterprise proxy.

**Demo:** [Watch the proxy demo](https://youtu.be/eLQQdQ6Njh8)

### Benchmarks

| Metric | Value |
|---|---|
| Inspection throughput | ~95.50 MB/sec |
| Peak heap (HeapAlloc) | 2.79 MB |
| Total system RAM | 13.29 MB |

### Quickstart

**Free trial** — 50 requests/day:
```bash
# Linux / macOS
./titan-shield -port 8080 -block=true

# Windows
.\titan-shield.exe -port 8080 -block=true
```

**Licensed:**
```bash
# Linux / macOS
./titan-shield -port 8080 -block=true -lic "YOUR_KEY"

# Windows
.\titan-shield.exe -port 8080 -block=true -lic "YOUR_KEY"
```

Point your application at `http://localhost:8080` instead of the AI endpoint directly. Titan-Shield inspects, scrubs, and forwards clean requests.

### Flags

| Flag | Description | Default |
|---|---|---|
| `-port` | Local port to listen on | 8080 |
| `-block` | Block requests that match rules (vs redact-and-forward) | false |
| `-lic` | Polar license key | — |

**Output:** Sanitized request forwarded to target endpoint, or 403 with a local audit log entry.

**[Get license →](https://buy.polar.sh/polar_cl_3N2hZ4KUDkX8CahsKSAdYJ7TwRggvXJctLUUJ2yvO4V)**

---

## Why Go binaries

Python-based alternatives (LangChain loaders, pydub, pandas dedup scripts) load entire datasets into memory and run single-threaded. These tools stream data through concurrent worker pools and stay under 80 MB RAM regardless of input size. No `pip install`, no virtualenv, no dependency conflicts. Download, unzip, run.

---

## Feedback & Bug Reports

Open an [issue on GitHub](https://github.com/vasudeval/vasudeval-labs/issues) or visit [vasudeval.com](https://vasudeval.com).

---

## License

Free trial binaries run without a key. Production use requires a node-locked license from [Polar](https://vasudeval.com). Each license is tied to one machine.
