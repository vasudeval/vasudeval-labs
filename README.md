# ⚡ Local AI Data Ingestion & Preprocessing Engines (Go CLI Utilities)

Welcome to the central command hub for **Vasudeva Labs** elite engineering utilities. We build ultra-fast, zero-dependency, local-first command-line interface (CLI) data pipelines and parsing tools designed to eliminate heavy SaaS cloud API overhead, guarantee absolute air-gapped data sovereignty, and run with minimal resource footprint on local developer hardware.

All premium production licenses, cross-compiled binaries, and hardware node activation keys are managed and distributed securely via Polar.

👉 **Acquire Production Licenses & Executables:** [Vasudeva Labs Polar Store](https://polar.sh/vasudeva-labs)

---

## 🛠️ Current Product Suite & Core Capabilities

### 📦 1. Titan-Doc CLI (Universal Flat-Memory Markdown Extraction Engine)
* **Core Functionality:** Ultra-high-speed native multi-format text parsing, recurring header/footer layout scrubbing, and complex table matrix structure flattening directly into clean standard Markdown (`|---|---|`).
* **Performance Metric:** Processes 181.06 MB of multi-format enterprise files in 2.40 seconds while capping peak memory consumption to a strict 3.56 MB flat profile.
* **Target Keywords:** PDF layout to Markdown, PDF table extractor CLI, docx table conversion, local data cleaning parser, unstructured data to Markdown table pipeline.
* **Licensing:** [Unlock Premium Doc Node Keys](https://polar.sh/vasudeva-labs)

### 📦 2. Titan-Ingest CLI (Local Document Parser & RAG Chunking Engine)
* **Core Functionality:** High-throughput local PDF/Markdown parsing, structural layout extraction, and semantic text chunking for vector database embeddings.
* **Performance Metric:** Processes 400+ complex technical documents per second natively via parallel Go channels under 50 MB RAM.
* **Target Keywords:** RAG data preparation, document parser CLI, local chunking tool, unstructured data to JSON, table extraction pipeline.
* **Licensing:** [Unlock Premium Ingest Node Keys](https://polar.sh/vasudeva-labs)

### 📦 3. Titan-Audio CLI (Local Media Stream Preprocessor for Whisper AI)
* **Core Functionality:** Direct-to-disk system codec streaming to automatically standardize batch video and audio folders into 16,000 Hz Mono Linear PCM WAV structures.
* **Performance Metric:** Maintains flat < 13 MB peak RAM allocation at 24.6x real-time streaming velocity.
* **Target Keywords:** Whisper AI audio preprocessing, audio converter CLI, batch WAV audio optimizer, local media ingestion engine, Go audio processing.
* **Licensing:** [Unlock Premium Audio Node Keys](https://polar.sh/vasudeva-labs)

### 📦 4. Titan-Forge CLI (Token-Aware Semantic Slicer & Compliance Scrubber)
* **Core Functionality:** Two-pass stream processor executing regular-expression PII scrubbing (emails, internal IPs, API secret tokens) on-the-fly, combined with layout-aware structural Markdown token slicing and rolling sliding-window context preservation.
* **Performance Metric:** Executes 40,000 security redactions across a 100,000-line chaotic data stream and generates 4,000 token-bounded chunks in 2.09 seconds under a 73.44 MB RAM peak footprint.
* **Target Keywords:** RAG security firewall, local PII scrubber CLI, token-aware chunking tool, cl100k_base tokenizer Go, air-gapped data compliance engine.
* **Licensing:** [Unlock Premium Forge Node Keys](https://polar.sh/vasudeva-labs)

---

## 📄 Titan-Doc CLI Execution Manual

Titan-Doc is our flagship zero-dependency, edge-first CLI pipeline engine written in pure Go. It is engineered specifically to eliminate data-leaking, per-page SaaS processing bills by extracting clean, structured text and dense matrix arrays out of deep enterprise archives (`.pdf`, `.docx`, `.xlsx`) and transforming them instantly into standardized Markdown code blocks for LLM contexts.

▶️ **[Watch the 181MB 2-Second Flat-Memory Titan-Doc Demo](https://youtu.be/noDs2xnzpJM)**

### ⚡ Verified Benchmark Telemetry (Live Production Metrics)
* **Source Catalog Payload Volume:** 181.06 MB
* **Extracted Export Markdown Volume:** 0.43 MB
* **Total Target Input Inventory:** 23 files (Dense PDFs, Docx Manuals, Xlsx Matrices)
* **Total Ingestion Duration:** 2.404539976 Seconds
* **Processing Stream Velocity:** 75.30 MB/sec
* **Peak Memory Allocation (HeapAlloc):** 3.56 MB (Strict Flat Memory Boundary)
* **Total System Memory Claimed:** 18.15 MB

### 🚀 Execution Syntax Reference

#### 🆓 Free Trial Mode (Bypass Licensing)
Omit the license flag to process up to 3 structural elements per document for rapid validation testing.
* **Linux / macOS:** `./titan-doc -in ./test_files -out ./markdown_outputs`
* **Windows PowerShell:** `.\titan-doc.exe -in .\test_files -out .\markdown_outputs`

#### 🔑 Premium Production Execution (Node-Locked Enterprise Mode)
Pass your Polar key string parameter to process unlimited directories recursively.
* **Linux / macOS:** `./titan-doc -in /path/to/source_dir -out /path/to/markdown_output -lic "POLAR_LICENSE_KEY"`
* **Windows PowerShell:** `.\titan-doc.exe -in "C:\source_dir" -out "C:\markdown_output" -lic "POLAR_LICENSE_KEY"`

---

## 📦 Titan-Ingest CLI Execution Manual

Titan-Ingest is a zero-dependency, ultra-fast command-line ingestion engine that extracts, parses, and semantically chunks local documentation at scale. Running 100% locally on your machine terminal, it guarantees absolute data sovereignty while delivering raw, compiled machine performance.

▶️ **[Watch the 60-Second Titan-Ingest 140x Performance Demo](https://youtu.be/aShsIDnLZRk)**

### 📦 Key Features & Engine Metrics
* **Blazing Throughput:** Processes 400+ complex technical documents per second recursively using native Go concurrent worker pool channels.
* **Air-Gapped Privacy:** 100% client-side data operations. Zero cloud internet dependencies required—private intellectual property and source code never leave your firewalls.
* **AI-Ready Structural Chunking:** Slices target data along semantic section boundaries and isolates tables row-by-row to ensure vector databases receive clean contexts, entirely preventing LLM hallucinations.

### 🚀 Execution Syntax Reference

#### 🆓 Free Trial Mode (Bypass Licensing)
* **Linux / macOS:** `./titan-ingest -in /path/to/flat_documents_folder`
* **Windows PowerShell:** `.\titan-ingest.exe -in "C:\path\to\flat_documents_folder"`

#### 🔑 Premium Production Execution (Node-Locked Enterprise Mode)
* **Linux / macOS:** `./titan-ingest -in /path/to/docs -out /path/to/nodes.json -lic "POLAR_KEY" -workers 4`
* **Windows PowerShell:** `.\titan-ingest.exe -in "C:\docs" -out "C:\nodes.json" -lic "POLAR_KEY" -workers 4`

---

## 🔊 Titan-Audio CLI Execution Manual

Titan-Audio is a zero-dependency, local-first CLI tool written in pure Go designed to rapidly prepare large directories of mixed media files (.mp4, .mkv, .wav, .mp3, .m4a) for local AI frameworks like Whisper.

Using optimized os/exec kernel streaming pipes, Titan-Audio keeps memory consumption low and flat (< 13 MB peak RAM), regardless of the input file size.

▶️ **[Watch the Titan-Audio Structural Preprocessing Demo](https://youtu.be/PKY7JPWxfLI)**

### ⚡ Verified Performance Metrics
* **Input Dataset Footprint:** 101.35 MB
* **Peak Memory Allocation:** 12.46 MB (Flat)
* **Core Engine Processing Velocity:** 24.6x Real-Time Speed
* **Concurrency Model:** Lock-Free Worker Pool

### 🛠️ Quickstart Usage Manual

#### 🆓 Free Trial Mode (Bypass Licensing)
* **Linux / macOS:** `./titan-audio -in ./your_media_dir -out ./whisper_ready`
* **Windows PowerShell:** `.\titan-audio.exe -in "C:\your_media_dir" -out "C:\whisper_ready"`

#### 🔑 Premium Production Execution (Node-Locked Enterprise Mode)
* **Linux / macOS:** `./titan-audio -in ./your_media_dir -workers 4 -lic "POLAR_LICENSE_KEY"`
* **Windows PowerShell:** `.\titan-audio.exe -in "C:\your_media_dir" -workers 4 -lic "POLAR_LICENSE_KEY"`

---

## 🛠️ Titan-Forge CLI Execution Manual

Titan-Forge is a zero-dependency, edge-first CLI pipeline engine built to act as an unbreachable local data security gate before document contents are routed to LLM vectors. It streams unstructured data through an inline PII regular-expression scrubbing layer while simultaneously calculating layout-aware chunk splits using a high-fidelity native BPE token estimation algorithm.

▶️ **[Watch the 100K-Line 40,000-Redaction Titan-Forge Demo](https://youtu.be/ZKgoJdrQJIE)**

### ⚡ Verified Benchmark Telemetry (Live Production Metrics)
* **Source Intake Stream Depth:** 100,000 Lines (Concurrently Loaded)
* **Dynamic Security Redactions:** 40,000 Assets (Emails, IPs, API Keys)
* **Total Generated Token Chunks:** 4,000 Semantic JSON Blocks
* **Execution Processing Time:** 2.093 Seconds
* **Processing Stream Velocity:** 19,112 Redactions/Sec
* **Peak Running RAM Baseline:** 73.44 MB (Strict Flat Streaming Memory Profile)

### 🚀 Execution Syntax Reference

#### 🆓 Free Trial Mode (Bypass Licensing)
Omit the license flag to process the first 5 files and up to 10 chunks per file (appends promotional checkout watermark comments to output blocks).
* **Linux / macOS:** `./titan-forge -in ./test_vault -out ./llm_ready_json/forge_chunks.json -size 500 -overlap 50`
* **Windows PowerShell:** `.\titan-forge.exe -in .\test_vault -out .\llm_ready_json\forge_chunks.json -size 500 -overlap 50`

#### 🔑 Premium Production Execution (Node-Locked Enterprise Mode)
Pass your Polar key string parameter to completely lift file caps and unlock recursive deep directory tree traversals.
* **Linux / macOS:** `./titan-forge -in /path/to/source_dir -out /path/to/output.json -size 500 -overlap 50 -lic "POLAR_LICENSE_KEY" -workers 4`
* **Windows PowerShell:** `.\titan-forge.exe -in "C:\source_dir" -out "C:\output.json" -size 500 -overlap 50 -lic "POLAR_LICENSE_KEY" -workers 4`

---
*Built for absolute privacy, local edge processing efficiency, and raw compiled execution speed by Vasudeva Labs.*
