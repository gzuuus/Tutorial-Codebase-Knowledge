# Tutorial: mcp-server-youtube-transcript

This project is a **YouTube Transcript Extractor** service that provides AI models with the ability to *request and receive transcripts* from YouTube videos. It implements the **Model Context Protocol (MCP)** specification, allowing AI models to seamlessly interact with the service through a standardized interface. The server accepts a YouTube URL or video ID plus an optional language code, extracts the unique video identifier, fetches the transcript using a third-party library, and returns the formatted text content. The system includes comprehensive **error handling** to manage invalid inputs and processing failures.


**Source Repository:** [https://github.com/kimtaeyoon83/mcp-server-youtube-transcript](https://github.com/kimtaeyoon83/mcp-server-youtube-transcript)

```mermaid
flowchart TD
    A0["YouTubeTranscriptExtractor
"]
    A1["TranscriptServer
"]
    A2["MCP Server Implementation
"]
    A3["Tool Configuration
"]
    A4["Error Handling System
"]
    A5["Request Handlers
"]
    A6["YouTube ID Extraction
"]
    A1 -- "Creates and utilizes" --> A0
    A1 -- "Initializes and manages" --> A2
    A2 -- "References during setup" --> A3
    A5 -- "Invokes methods on" --> A0
    A5 -- "Utilizes for failures" --> A4
    A0 -- "Implements and uses" --> A6
    A0 -- "Throws errors using" --> A4
```

## Chapters

1. [MCP Server Implementation
](01_mcp_server_implementation_.md)
2. [TranscriptServer
](02_transcriptserver_.md)
3. [YouTubeTranscriptExtractor
](03_youtubetranscriptextractor_.md)
4. [YouTube ID Extraction
](04_youtube_id_extraction_.md)
5. [Request Handlers
](05_request_handlers_.md)
6. [Error Handling System
](06_error_handling_system_.md)
7. [Tool Configuration
](07_tool_configuration_.md)


---

Generated by [AI Codebase Knowledge Builder](https://github.com/The-Pocket/Tutorial-Codebase-Knowledge)