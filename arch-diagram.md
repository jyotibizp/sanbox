Here’s a **Mermaid diagram** to visualize your architecture using **Azure Durable Functions orchestration**, ADF, Snowflake, and Azure Blob.

---

### ✅ **Architecture: Azure Durable Functions Orchestrating Salesforce → Snowflake → Validation Flow**

```mermaid
flowchart TD

    %% Trigger Start
    A1[HTTP Trigger or Timer Trigger] --> O1

    %% Durable Orchestrator
    O1[Durable Orchestrator Function]

    %% Step 1: Trigger ADF Pipeline
    O1 --> ADF[Activity: Trigger ADF Pipeline]
    ADF --> SF1[Snowflake: Delta Tables]

    %% Step 2: Parse Delete Logs
    O1 --> PARSE[Activity: Parse delete-logs.db]
    PARSE --> BLOB1[Blob Storage: delete-logs.db (SQLite)]
    PARSE --> SF2[Snowflake: Delete Tracker Table]

    %% Step 3: Wait for Downstream Report
    O1 --> WAIT[Activity: Wait for Downstream Report Blob]
    WAIT --> BLOB2[Blob Storage: Downstream Report]

    %% Step 4: Run Validation
    O1 --> VALIDATE[Activity: Run Data Validation]
    VALIDATE --> SF3[Snowflake: Processed Data]
    VALIDATE --> BLOB2

    %% Step 5: Save Validation Report
    VALIDATE --> REPORT[Generate Validation Report (Excel)]
    REPORT --> UPLOAD[Activity: Upload Report to Blob]
    UPLOAD --> BLOB3[Blob Storage: Validation Report (Excel)]

    %% Styling (optional: ignored in GitHub but useful in Mermaid Live)
    classDef blob fill:#d9d2e9,stroke:#6a329f;
    classDef snowflake fill:#f4cccc,stroke:#cc0000;
    classDef func fill:#cfe2f3,stroke:#3c78d8;
    class ADF,PARSE,WAIT,VALIDATE,UPLOAD func;
    class SF1,SF2,SF3 snowflake;
    class BLOB1,BLOB2,BLOB3 blob;
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

