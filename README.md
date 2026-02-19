graph TB
  subgraph L1["Layer 1: Presentation"]
    UI[React Dashboard<br/>Goal Input + Progress]
    API[REST/WebSocket API]
  end
  
  subgraph L2["Layer 2: Orchestration & Agents"]
    ORCH[System Orchestrator<br/>LangChain + State Mgmt]
    PLANNER[Planner Agent<br/>CurriculumJSON]
    RESEARCH[Research Agent<br/>RankedResourceList]
    TUTOR[Tutor Agent<br/>Explanation + Quiz]
    QA[QA Agent<br/>QAReport]
  end
  
  subgraph L3["Layer 3: Infrastructure"]
    PG[PostgreSQL<br/>SessionState]
    CHROMA[ChromaDB/Pinecone<br/>RAG Embeddings]
    REDIS[Redis<br/>Cache + Pub/Sub]
    TOOLS[SerpAPI/arXiv/YouTube]
  end
  
  UI --> API --> ORCH
  ORCH --> PLANNER
  PLANNER -.->|P2P| RESEARCH
  ORCH --> RESEARCH
  ORCH --> TUTOR
  ORCH --> QA
  PLANNER --> PG
  RESEARCH --> CHROMA
  TUTOR --> CHROMA
  QA --> PG
  ORCH --> REDIS
  RESEARCH --> TOOLS[file:41]
  
  classDef orchestrator fill:#ff9,stroke:#333,stroke-width:3px
  class ORCH orchestrator
