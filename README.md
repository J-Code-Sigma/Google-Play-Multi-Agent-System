================================================================================
PROJECT: DISTRIBUTED A2A RESEARCH CLUSTER
FILE: README.md
================================================================================

# Scraper-Powered Multi-Agent Research Squad (A2A Distributed)

This project implements a Distributed Multi-Agent System (MAS) that leverages the **A2A Protocol** to automate product research, market gap analysis, and PRD generation across a heterogeneous compute cluster.

By offloading "grunt work" to local legacy hardware and "high-reasoning" to cloud models, the system optimizes for both cost and intelligence.

## Architecture

The system is decentralized. Instead of a single master script, each node acts as a specialist service communicating via **JSON-RPC 2.0**. A central Gateway (Pi 5) handles task routing based on hardware capability.



```mermaid
graph TD
    %% Nodes
    User((User))
    Gateway["<b>The Gateway (Pi 5)</b><br/>A2A Router & Discovery<br/>(Task Distribution)"]
    
    subgraph Local_Compute_Cluster["Local A2A Fleet"]
        Orchestrator["<b>The Orchestrator (G16)</b><br/>Llama 3.2 8B<br/>(Logic & Reasoning)"]
        Librarian["<b>The Librarian (ITX)</b><br/>Mistral 7B / Vector DB<br/>(Knowledge & RAG)"]
        Scout["<b>The Scout (GTX 960)</b><br/>Llama 3.2 1B / Play Scraper<br/>(Data Extraction)"]
    end

    subgraph Cloud_Tier["Cloud Intelligence"]
        Analyst["<b>The Analyst</b><br/>Claude Sonnet 4.5<br/>(Market Gap Analysis)"]
        Architect["<b>The Architect</b><br/>Gemini 3 Pro<br/>(PRD & Build Plan)"]
    end

    %% Flow
    User -->|Define Topic| Gateway
    Gateway -->|Delegate| Orchestrator
    Orchestrator -->|Request Scrape| Scout
    Scout -->|Return Raw Data| Librarian
    Librarian -->|Contextualize| Orchestrator
    Orchestrator -->|Evaluate Case| Analyst
    Analyst -->|Define Concept| Architect
    Architect -->|Final PRD| User

    %% Styling
    style Gateway fill:#C51A4A,stroke:#fff,color:#fff
    style Orchestrator fill:#4285F4,stroke:#fff,color:#fff
    style Librarian fill:#34A853,stroke:#fff,color:#fff
    style Scout fill:#333,stroke:#fff,color:#fff
    style Analyst fill:#D97757,stroke:#fff,color:#fff
    style Architect fill:#4285F4,stroke:#fff,color:#fff
```

# Distributed A2A Fleet Overview

## The Fleet (Hardware & Roles)

| Node | Role | Hardware | Primary Model / Tool |
| :--- | :--- | :--- | :--- |
| **Gateway** | Task Routing / Discovery | Raspberry Pi 5 | A2A Router (FastAPI) |
| **Orchestrator** | Logic / Reasoning | ASUS ROG G16 | Llama 3.2 8B |
| **Librarian** | Context / RAG | Mini-ITX (RTX 3050) | Mistral 7B + ChromaDB |
| **Scout** | Web Scraping / Grunt Work | Desktop (GTX 960) | Llama 3.2 1B + Play Scraper |
| **Cloud Tier** | Synthesis & Final Design | AWS/Google/Anthropic | Claude 4.5 / Gemini 3 Pro |

---

## The Protocol: A2A (Agent-to-Agent)
All nodes adhere to the A2A communication standard to ensure the cluster remains modular and scalable.

* **Discovery**: Each node hosts an Agent Card at `/.well-known/agent.json` defining its capabilities (e.g., `web_scrape`, `vector_search`).
* **Communication**: Task requests and results are exchanged via **JSON-RPC 2.0** over HTTP.
* **Statelessness**: Workers are stateless; the **Orchestrator (G16)** maintains the session state, while the **Librarian (ITX)** maintains the long-term knowledge base.

---

## The Research Loop
1.  **Scout (GTX 960)**: Executes raw data extraction from the Google Play Store using custom scrapers.
2.  **Librarian (ITX)**: Cleans the data, generates embeddings, and stores them in a local vector database for rapid retrieval.
3.  **Orchestrator (G16)**: Queries the Librarian to identify trends and coordinates with the Cloud Tier for deep analysis.
4.  **Strategist (Cloud)**: Performs the final "Heavy Lifting"—identifying viable market gaps (**Claude 4.5**) and drafting the technical PRD (**Gemini 3 Pro**).

---

## Integration Notes
* **Networking**: All local nodes must be on the same subnet with static IP assignments or local DNS resolution (e.g., `scout.local`).
* **Security**: Internal A2A traffic is unauthenticated for performance, but the Gateway acts as the firewall for external requests.