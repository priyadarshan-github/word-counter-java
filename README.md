flowchart TB

    U[End Users / Employees / SMEs]

    subgraph P[Presentation Layer]
        AA[Apache Answer UI\nQ&A Portal / Knowledge Hub]
    end

    subgraph A[Application & AI Orchestration Layer]
        APIGW[API Gateway / Backend Service\nFastAPI or Spring Boot]
        AUTH[Auth / SSO / RBAC]
        ORCH[AI Orchestrator]
        DUP[Duplicate Question Detector]
        TAG[Auto Tagging / Classification]
        CONF[Confidence Scoring]
        FEED[Feedback & Review Workflow]
    end

    subgraph R[Retrieval & Search Layer]
        SEARCH[Hybrid Search Service\nKeyword + Semantic Search]
        VDB[(Vector Store / Embedding Index)]
        ES[(Elasticsearch / OpenSearch)]
        META[(Metadata DB - PostgreSQL)]
    end

    subgraph I[Ingestion & Processing Layer]
        INGEST[Ingestion Service]
        PARSER[Document Parser / Chunker]
        EMBED[Embedding Generator]
        SYNC[Scheduler / Sync Jobs]
    end

    subgraph S[Enterprise Knowledge Sources]
        CONFL[Confluence]
        SHARE[SharePoint / Wiki Pages]
        PDF[PDF / DOCX / SOPs]
        GIT[GitHub / Bitbucket Repos]
        DB[Operational DB / Knowledge Tables]
        QA[Apache Answer Historical Q&A]
    end

    subgraph L[LLM Layer]
        GEM[Gemini API\nAnswer Generation / Summarization / Reasoning]
    end

    U --> AA
    AA --> APIGW
    APIGW --> AUTH
    APIGW --> ORCH

    ORCH --> DUP
    ORCH --> TAG
    ORCH --> SEARCH
    ORCH --> CONF
    ORCH --> FEED
    ORCH --> GEM

    SEARCH --> VDB
    SEARCH --> ES
    SEARCH --> META
    SEARCH --> QA

    CONFL --> INGEST
    SHARE --> INGEST
    PDF --> INGEST
    GIT --> INGEST
    DB --> INGEST
    QA --> INGEST

    INGEST --> PARSER
    PARSER --> EMBED
    EMBED --> VDB
    PARSER --> ES
    PARSER --> META
    SYNC --> INGEST

    SEARCH --> GEM
    META --> GEM

    GEM --> ORCH
    ORCH --> APIGW
    APIGW --> AA
    AA --> U
