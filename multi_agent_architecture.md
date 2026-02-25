# Scraper-Powered Multi-Agent Research Squad (A2A Distributed)

This project implements a Distributed Multi-Agent System (MAS) that leverages the A2A Protocol to automate product research, market gap analysis, and PRD generation across a heterogeneous compute cluster.

## Architecture

The system is decentralized. Instead of a single master script, each node acts as a specialist service communicating via JSON-RPC 2.0. A central Gateway handles task routing based on hardware capability and current load.

### Scraper-Powered Research Squad Architecture

This diagram visualizes the updated "Loop": Local Scout -> Analyst -> Architect, distributed across the hardware fleet.

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