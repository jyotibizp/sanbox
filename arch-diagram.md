Here’s a **Mermaid diagram** to visualize your architecture using **Azure Durable Functions orchestration**, ADF, Snowflake, and Azure Blob.

---

### ✅ **Architecture: Azure Durable Functions Orchestrating Salesforce → Snowflake → Validation Flow**

```mermaid
flowchart TD
    subgraph Trigger
        A1(HTTP Trigger<br/>or Timer Trigger)
    end

    subgraph DurableOrchestrator
        O1[Durable Orchestrator Function]
        O1 --> ADF[Activity: Trigger ADF Pipeline]
        ADF --> SF1[Snowflake Delta Tables]
        
        O1 --> PARSE[Activity: Parse delete-logs.db]
        PARSE --> BLOB1[Azure Blob<br/>delete-logs.db]
        PARSE --> SF2[Insert to Snowflake<br/>Delete Tracker Table]
        
        O1 --> WAIT[Activity: Wait for Downstream Report Blob]
        WAIT --> BLOB2[Azure Blob<br/>Downstream Report]

        O1 --> VALIDATE[Activity: Run Data Validation]
        VALIDATE --> SF3[Snowflake Processed Data]
        VALIDATE --> BLOB2

        VALIDATE --> REPORT[Validation Report (Excel)]

        O1 --> UPLOAD[Activity: Upload Validation Report]
        UPLOAD --> BLOB3[Azure Blob<br/>Validation Report]
    end

    style DurableOrchestrator fill:#fdf6e3,stroke:#b58900,stroke-width:2px
    style Trigger fill:#d9ead3,stroke:#38761d,stroke-width:1px
    style ADF fill:#cfe2f3,stroke:#3c78d8
    style PARSE fill:#cfe2f3,stroke:#3c78d8
    style WAIT fill:#cfe2f3,stroke:#3c78d8
    style VALIDATE fill:#cfe2f3,stroke:#3c78d8
    style UPLOAD fill:#cfe2f3,stroke:#3c78d8

    style SF1 fill:#f4cccc,stroke:#cc0000
    style SF2 fill:#f4cccc,stroke:#cc0000
    style SF3 fill:#f4cccc,stroke:#cc0000

    style BLOB1 fill:#d9d2e9,stroke:#6a329f
    style BLOB2 fill:#d9d2e9,stroke:#6a329f
    style BLOB3 fill:#d9d2e9,stroke:#6a329f
    style REPORT fill:#ead1dc,stroke:#a64d79
```

---

### 📝 How to Use This

You can render this in:

* [Mermaid Live Editor](https://mermaid.live/edit)
* Markdown files in VS Code with Mermaid support
* GitHub README (within a supported code block)
* Azure DevOps Wikis

---

Let me know if you want a **static image (PNG/SVG)** version or a version that includes **error-handling/monitoring paths** (like retries, alerts, etc.).

