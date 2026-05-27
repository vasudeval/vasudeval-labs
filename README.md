# Titan Series — Local AI Data Preprocessing Engines

Six zero-dependency Go CLI tools for LLM data preprocessing. Run locally, no cloud calls, no Python overhead.

Built for developers who need to prepare documents, audio, and text datasets for LLM pipelines without paying per-page SaaS fees or fighting Python memory limits.

**Website:** [vasudeval.com](https://vasudeval.com) | **Demo videos:** linked per tool below

---

## Tools at a Glance

| Tool | What it does | RAM | Speed |
|---|---|---|---|
| [Titan-Doc](#titan-doc) | PDF/DOCX/XLSX → clean Markdown | 3.56 MB heap | 75.30 MB/sec |
| [Titan-Ingest](#titan-ingest) | Documents → chunked JSON for vector DBs | < 50 MB | 400+ docs/sec |
| [Titan-Audio](#titan-audio) | Audio/video → Whisper-ready WAV | < 13 MB | 24.6x realtime |
| [Titan-Forge](#titan-forge) | Markdown → PII-scrubbed token chunks | 73.44 MB | 19,112 redactions/sec |
| [Titan-Purge](#titan-purge) | Text datasets → deduplicated corpus | < 22 MB | 128-bit MinHash LSH |
| [Titan-Shield](#titan-shield) | Local DLP proxy for AI API calls | 2.79 MB heap | ~95.50 MB/sec inspection |

All tools:
- Single static binary, no runtime dependencies
- Free trial mode works without a license key (limits noted per tool)
- Licensed via [Polar](https://vasudeval.com) for production use

---

## Download

Go to [Releases](https://github.com/vasudeval/vasudeval-labs/releases/latest) and download the binary for your platform.

**Linux (amd64)**
```bash
curl -L https://github.com/vasudeval/vasudeval-labs/releases/latest/download/titan-doc-linux-amd64 -o titan-doc
chmod +x titan-doc
./titan-doc -in ./test_files -out ./output
```

**macOS (Apple Silicon)**
```bash
curl -L https://github.com/vasudeval/vasudeval-labs/releases/latest/download/titan-doc-darwin-arm64 -o titan-doc
chmod +x titan-doc
./titan-doc -in ./test_files -out ./output
```

**Windows (PowerShell)**
```powershell
Invoke-WebRequest -Uri "https://github.com/vasudeval/vasudeval-labs/releases/latest/download/titan-doc-windows-amd64.exe" -OutFile "titan-doc.exe"
.\titan-doc.exe -in .\test_files -out .\output
```

Replace `titan-doc` with the tool name you want (`titan-ingest`, `titan-audio`, etc.).

---

## Titan-Doc

**PDF / DOCX / XLSX → clean Markdown**

Extracts text and tables from document files into flat Markdown. Strips recurring headers, footers, and page numbers during extraction. Tables become standard `|---|---|` Markdown, not broken prose.

**Demo:** [Watch 181MB processed in 2.4 seconds](https://youtu.be/noDs2xnzpJM)

### Benchmarks

| Metric | Value |
|---|---|
| Input processed | 181.06 MB (23 files: PDFs, DOCX, XLSX) |
| Output | 0.43 MB clean Markdown |
| Duration | 2.40 seconds |
| Throughput | 75.30 MB/sec |
| Peak heap (HeapAlloc) | 3.56 MB |
| Total system RAM | 18.15 MB |

### Usage

**Free trial** (no license needed — processes up to 3 pages/rows per file):
```bash
# Linux / macOS
./titan-doc -in ./test_files -out ./markdown_outputs

# Windows
.\titan-doc.exe -in .\test_files -out .\markdown_outputs
```

**Licensed** (unlimited files, recursive directories):
```bash
# Linux / macOS
./titan-doc -in /path/to/source_dir -out /path/to/output -lic "YOUR_KEY"

# Windows
.\titan-doc.exe -in "C:\source_dir" -out "C:\output" -lic "YOUR_KEY"
```

**[Get license key →](https://buy.polar.sh/polar_cl_OCEX5FlOytMtbV48UZ2LVUD1vJtPJ01RwTz4t05IVVu)**

### Inputs / Outputs

- **Input:** Directory of `.pdf`, `.docx`, `.xlsx` files
- **Output:** One `.md` file per document, tables preserved as Markdown

---

## Titan-Ingest

**Documents → chunked JSON for vector databases**

Parses PDF, HTML, and text files and splits them into semantic chunks for embedding. Splits at natural boundaries (headings, table rows) rather than fixed character counts. Outputs a single JSON file ready for ingestion into Pinecone, Weaviate, Chroma, or any vector DB.

**Demo:** [Watch the 140x performance demo](https://youtu.be/aShsIDnLZRk)

### Benchmarks

| Metric | Value |
|---|---|
| Throughput | 400+ complex technical docs/sec |
| Peak RAM | < 50 MB |
| Concurrency | Lock-free parallel Go worker pool |

### Usage

**Free trial** (up to 20 files, 30 pages per file):
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

**[Get license key →](https://buy.polar.sh/polar_cl_7JmTYuEIzOK6nHnWrlUt9Q8l2kmT4LOQO6Syd26xemD)**

### Inputs / Outputs

- **Input:** Directory of `.pdf`, `.html`, `.txt` files. Optional: `-workers N` to set concurrency.
- **Output:** `ingested_nodes.json` — array of chunks with content, source metadata, and a hash per chunk.

---

## Titan-Audio

**Audio and video → Whisper-ready WAV**

Converts any mix of `.mp4`, `.mkv`, `.wav`, `.mp3`, `.m4a` files to 16kHz mono linear PCM WAV — the exact format Whisper expects. Runs FFmpeg as a kernel pipe (not a Python subprocess), keeping RAM flat regardless of input file size. Outputs a JSON manifest with per-file metrics (duration, peak dB, sample rate).

**Demo:** [Watch the preprocessing demo](https://youtu.be/PKY7JPWxfLI)

### Benchmarks

| Metric | Value |
|---|---|
| Input dataset | 101.35 MB |
| Peak RAM | 12.46 MB (flat) |
| Processing speed | 24.6x realtime |
| Concurrency | Lock-free worker pool |

> **Note:** Requires FFmpeg installed on the system (`brew install ffmpeg` / `apt install ffmpeg`).

### Usage

**Free trial** (up to 5 files, 10 min/file max):
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

**[Get license key →](https://buy.polar.sh/polar_cl_fjnkoggFxnnlaqSwuhVXHGNk025W1LngmCSOh1yM6N0)**

### Inputs / Outputs

- **Input:** Directory of audio/video files (`.mp4`, `.mkv`, `.wav`, `.mp3`, `.m4a`)
- **Output:** `.wav` files at 16kHz, mono, 16-bit PCM + `manifest.json` with per-file stats

---

## Titan-Forge

**Markdown/text → PII-scrubbed, token-bounded JSON chunks**

Two-pass stream processor. First pass: regex scrubbing for emails, IP addresses, and API key patterns. Second pass: splits into token-bounded chunks with configurable size and overlap using a BPE-compatible tokenizer. Outputs chunks with parent heading context preserved.

Everything runs locally — no data leaves the machine.

**Demo:** [Watch 100K lines, 40K redactions in 2 seconds](https://youtu.be/ZKgoJdrQJIE)

### Benchmarks

| Metric | Value |
|---|---|
| Input | 100,000 lines with 40,000 injected PII patterns |
| Redactions | 40,000 (emails, IPs, API keys) |
| Chunks generated | 4,000 token-bounded blocks |
| Duration | 2.09 seconds |
| Redaction rate | 19,112 redactions/sec |
| Peak RAM | 73.44 MB |

### Usage

**Free trial** (5 files max, 10 chunks per file, watermark appended to output):
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

**Flags:**

| Flag | Description | Default |
|---|---|---|
| `-in` | Input directory of `.md` or `.txt` files | required |
| `-out` | Output JSON file path | required |
| `-size` | Max tokens per chunk | 500 |
| `-overlap` | Token overlap between chunks | 50 |
| `-workers` | Parallel workers (licensed only) | 1 |
| `-lic` | Polar license key | — |

**[Get license key →](https://buy.polar.sh/polar_cl_ozDCIe3MbuW1R4MwIOp5cFF9nBCN5VNq48O5K1aRTHB)**

### Inputs / Outputs

- **Input:** Directory of `.md` or `.txt` files
- **Output:** `forge_chunks.json` — array of chunks with scrubbed content, token count, parent heading, and source file

---

## Titan-Purge

**Text dataset deduplication using MinHash LSH**

Computes 128-band MinHash signatures via Murmur3 for every file in a directory, then runs pairwise Jaccard similarity. Flags exact duplicates (100% match) and near-duplicates (≥ 85% similarity) in a JSON manifest. Operates entirely offline.

Use before building a vector index or fine-tuning dataset to avoid indexing redundant content.

**Demo:** [Watch the LSH deduplication demo](https://youtu.be/4vsMBnLZ2aw)

### Benchmarks

| Metric | Value |
|---|---|
| Peak RAM | < 22 MB |
| Hash matrix | 128-bit Murmur3 seeds |
| Similarity threshold | ≥ 85% Jaccard |
| Concurrency | Non-blocking parallel worker pool |

### Usage

**Free trial** (up to 5 files, no directory recursion):
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

**[Get license key →](https://buy.polar.sh/polar_cl_PNYfBKzakuI0ZHPu0LNNUaOmUnBzEMPDU3aAY0KpmaF)**

### Inputs / Outputs

- **Input:** Directory of `.txt`, `.log`, `.json`, `.csv`, or `.md` files
- **Output:** `purge_manifest.json` — duplicate pairs flagged with Jaccard scores, plus a deduplicated file list

---

## Titan-Shield

**Local reverse proxy that scrubs sensitive data from outbound AI API calls**

Sits between your application and any LLM API endpoint (OpenAI, Anthropic, etc.). Inspects the JSON payload, applies regex rules against field values, and either redacts matched patterns before forwarding or blocks the request entirely with a 403. Sub-millisecond inspection. All rules and logs stay local.

Useful for teams where developers are sending internal code, credentials, or customer data to hosted AI endpoints.

**Demo:** [Watch the proxy demo](https://youtu.be/eLQQdQ6Njh8)

### Benchmarks

| Metric | Value |
|---|---|
| Inspection throughput | ~95.50 MB/sec |
| Peak heap (HeapAlloc) | 2.79 MB |
| Total system RAM | 13.29 MB |

### Usage

**Free trial** (50 requests/day):
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

Point your app at `http://localhost:8080` instead of the AI endpoint directly. Titan-Shield forwards clean requests to the real endpoint.

**[Get license key →](https://buy.polar.sh/polar_cl_3N2hZ4KUDkX8CahsKSAdYJ7TwRggvXJctLUUJ2yvO4V)**

### Inputs / Outputs

- **Input:** Outbound JSON API requests on the configured local port, plus a rules file defining patterns to block/redact
- **Output:** Sanitized request forwarded to target endpoint, or 403 response with local audit log entry

---

## Why Go binaries

Python-based alternatives (LangChain loaders, pydub, pandas dedup scripts) load entire datasets into memory and run single-threaded. These tools stream data through worker pools and stay under 80 MB RAM regardless of input size. No pip install, no venv, no dependency conflicts — download and run.

---

## License

Free trial binaries are available without a key. Production use requires a node-locked license from [Polar](https://vasudeval.com).

Each license is tied to one machine. [Contact](https://vasudeval.com) for multi-seat or team pricing.
