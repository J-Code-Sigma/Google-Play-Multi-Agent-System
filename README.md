# Scraper-Powered Multi-Agent Research Squad

This project implements a Multi-Agent System (MAS) that combines low-cost local hardware with high-intelligence cloud models to automate product research and gap analysis.

## Architecture

The system uses a tiered approach to balance cost and intelligence:

```mermaid
graph TD
    %% Subgraphs
    subgraph Local_Tier["Local Tier (GTX 960)"]
        Scout[("<b>The Scout</b><br/>Llama 3.2 (via llama-cpp)<br/>+ Google Play Scraper")]
        style Scout fill:#333,stroke:#fff,stroke-width:2px,color:#fff
    end

    subgraph Cloud_Intelligence["Cloud Tier: High Intelligence"]
        direction TB
        Analyst["<b>The Analyst</b><br/>Claude Sonnet 4.5<br/>(Product Determination)"]
        Architect["<b>The Architect</b><br/>Gemini 3 Pro<br/>(PRD & Build Plan)"]
        
        style Analyst fill:#D97757,stroke:#fff,stroke-width:0px,color:#fff
        style Architect fill:#4285F4,stroke:#fff,stroke-width:0px,color:#fff
    end

    %% Flow
    Start((Start)) --> Scout
    Scout -- "Raw Details" --> Analyst
    Analyst -- "Product Concept" --> Architect
    Architect -- "PRD & Build Plan" --> Output((Done))

    %% Styling
    linkStyle default stroke:#aaa,stroke-width:2px,color:#aaa;
```

## The Stack

- **Local "Grunt Work"**: `Llama 3.2` running on a GTX 960 via `llama-cpp`. Handles initial scraping and filtering of the Google Play Store.
- **Analysis**: `Claude Sonnet 4.5`. Digs through the "Scout's" findings to identify viable market gaps.
- **Architecture**: `Gemini 3 Pro`. Takes the validated concept and generates a comprehensive PRD and implementation plan.

## The Loop

1. **Scout**: Hits the Play Store using custom scraping tools to gather raw app data.
2. **Analyst**: Reviews the scraped data to determine if a good product opportunity exists.
3. **Architect**: If a business case is confirmed, drafts the PRD and build plan.
# Google-Play-Multi-Agent-System
