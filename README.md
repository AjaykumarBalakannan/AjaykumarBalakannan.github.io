
**(The above block should NOT be indented. There should be no extra spaces/tabs before the triple backticks.)**

---

### **What To Do:**

1. **Edit your README.md** to ensure the mermaid block is not indented and is correctly formatted.
2. **Do NOT use `<br>` HTML tags inside Mermaid nodes**—use plain text.  
   - For example, replace  
     `A[Python Script<br>Fetch Bitcoin Price<br>via CoinGecko API]`  
     with  
     `A[Python Script: Fetch Bitcoin Price via CoinGecko API]`
3. **Commit and push** your changes again.
4. **Refresh your GitHub page** (you might need a hard refresh: `Ctrl+Shift+R`).

---

### **Copy-paste This Working Example**

```markdown
## Workflow & Architecture

### High-Level Workflow

```mermaid
graph TD
    A[Python Script: Fetch Bitcoin Price via CoinGecko API] --> B[Write Data to CSV]
    B --> C[Push CSV Files to GitHub]
    C --> D[Qlik Sense REST Connector: Pull Latest CSV from GitHub]
    D --> E[Qlik Sense Dashboard: Visualize & Analyze Data]
    E --> F[User Exploration: Filtering, Analytics, Interactive Charts]
    style A fill:#bbf,stroke:#222,stroke-width:2px
    style E fill:#cfc,stroke:#222,stroke-width:2px
    style F fill:#ffe,stroke:#222,stroke-width:1px
