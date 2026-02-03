# Scraper-Powered Research Squad Architecture

This diagram visualizes the updated "Loop": Local Scout -> Analyst -> Architect.

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
