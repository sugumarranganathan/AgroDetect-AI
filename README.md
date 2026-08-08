# 🌾 AgroDetect AI

## MCP-Powered Autonomous Agricultural Intelligence & Root-Cause Analysis

AgroDetect AI is an autonomous agricultural data-intelligence system
that analyzes crop data and answers natural-language questions through a
multi-agent workflow.

The system combines **Groq LLM, LangChain, LangGraph, MCP,
Python/Pandas, Matplotlib, and Gradio** to create an AI agricultural
analyst that can inspect data, plan an investigation, generate analysis
code, execute it through MCP, recover from coding errors, investigate
potential contributing factors, create visualizations, and produce a
final report.

> **Note:** The current project uses a synthetic/demo agricultural
> dataset created for demonstrating the AI workflow. It is not a source
> of real-world agricultural statistics.

------------------------------------------------------------------------

#  Problem Statement

Agricultural datasets contain many interconnected factors such as crop
type, region, soil type, rainfall, temperature, soil moisture,
fertilizer usage, irrigation, pest level, and crop yield.

Traditional data analysis often requires a person to:

1.  Inspect the dataset.
2.  Decide what analysis is required.
3.  Write Python code.
4.  Execute the code.
5.  Debug errors.
6.  Compare results.
7.  Create charts.
8.  Interpret the findings.
9.  Prepare a final report.

This process can be time-consuming and requires technical data-analysis
skills.

### Proposed Solution

**AgroDetect AI** automates this analytical workflow using specialized
AI agents.

A user can simply ask:

> "Why is crop yield lower in some regions?"

or:

> "What is the average rainfall?"

The system determines the appropriate analysis, accesses the
agricultural data through MCP tools, generates and executes Python
analysis code, handles coding failures through a controlled debugging
process, analyzes potential contributing factors, creates
visualizations, and returns an understandable answer.

------------------------------------------------------------------------

# Project Objective

The main objective is to build an **autonomous agricultural data
analyst** that can:

-   Understand natural-language agricultural questions.
-   Access agricultural data through MCP.
-   Plan appropriate data investigations.
-   Analyze numerical and categorical variables.
-   Generate Python analysis code automatically.
-   Execute analysis through MCP tools.
-   Detect and recover from coding errors.
-   Identify potential factors associated with crop yield.
-   Detect unusual observations.
-   Generate agricultural charts.
-   Produce a clear final report.
-   Provide answers through a Gradio chatbot interface.

------------------------------------------------------------------------

# 🧠 Core Architecture

``` text
                         👨‍🌾 USER
                            │
                            ▼
                    🌾 AgroDetect AI
                            │
                            ▼
                       Groq LLM
                            │
                            ▼
                       LangChain
                            │
                            ▼
                       LangGraph
                            │
             ┌──────────────┴──────────────┐
             ▼                             ▼
       🧠 Planner Agent              MCP Client
             │                             │
             ▼                             ▼
     🔍 Data Analyst Agent          MCP Server
             │                             │
             ▼                    Agricultural Tools
      👨‍💻 Coding Agent                    │
             │                             │
             ▼                             │
       Python Analysis ◄──────────────────┘
             │
             ▼
        ⚙️ MCP Execution
             │
        ┌────┴────┐
        │         │
      ERROR     SUCCESS
        │         │
        ▼         ▼
 🛠️ Debugging  🔎 Root-Cause
    Agent         Agent
        │         │
        └────┬────┘
             ▼
      📊 Visualization
          Agent
             │
             ▼
        📝 Report Agent
             │
             ▼
        FINAL ANSWER
             │
             ▼
        💬 Gradio UI
```

------------------------------------------------------------------------

# 🤖 AI Agents

AgroDetect AI currently uses **7 focused agents**.

  -----------------------------------------------------------------------
  \#                      Agent                   Responsibility
  ----------------------- ----------------------- -----------------------
  1                       🧠 Planner Agent        Creates an
                                                  investigation plan from
                                                  the user's question

  2                       🔍 Data Analyst Agent   Understands the dataset
                                                  and identifies
                                                  important variables

  3                       👨‍💻 Coding Agent         Generates Python
                                                  analysis code
                                                  dynamically

  4                       🛠️ Debugging Agent      Diagnoses failed code
                                                  and generates corrected
                                                  code

  5                       🔎 Root-Cause Analysis  Identifies potential
                          Agent                   factors associated with
                                                  the requested outcome

  6                       📊 Visualization Agent  Creates agricultural
                                                  charts

  7                       📝 Report Agent         Converts the analysis
                                                  into a readable final
                                                  report
  -----------------------------------------------------------------------

The project deliberately uses a smaller number of focused agents rather
than a large 16-agent architecture.

------------------------------------------------------------------------

# 🔌 Why MCP Is Used

MCP provides a standardized way for the AI workflow to access tools.

In AgroDetect AI, MCP exposes agricultural operations such as:

``` text
agro_system_status()
get_crop_dataset_summary()
get_crop_statistics()
get_missing_value_analysis()
execute_agricultural_analysis()
create_agricultural_chart()
```

The important architecture is:

``` text
Groq
  ↓
LangGraph
  ↓
Agent
  ↓
MCP Client
  ↓
MCP Server
  ↓
Agricultural Tool
  ↓
Result
  ↓
Agent
```

This separates the AI's reasoning from the tools that provide data and
execute analysis.

------------------------------------------------------------------------

# 🔄 Autonomous Coding & Debugging

One of the key features is the controlled autonomous coding loop.

``` text
Coding Agent
     ↓
Generate Python Code
     ↓
MCP Execution
     ↓
Code Successful?
   ↙          ↘
 YES          NO
  ↓            ↓
Continue    Debugging Agent
               ↓
          Correct the code
               ↓
          MCP Execution
               ↓
            Retry
```

The project uses a **maximum retry limit of 3 attempts**.

There is no infinite loop.

If the system cannot recover within the allowed attempts, the workflow
stops safely.

------------------------------------------------------------------------

# 📊 Agricultural Dataset

The current demo dataset contains:

-   **1,200 records**
-   **12 columns**
-   **24 missing values**

### Columns

  Column                          Description
  ------------------------------- ------------------------
  `Region`                        Agricultural region
  `Crop`                          Crop type
  `Soil_Type`                     Soil category
  `Irrigation_Type`               Irrigation method
  `Rainfall_mm`                   Rainfall
  `Temperature_C`                 Temperature
  `Humidity_Percent`              Humidity
  `Soil_Moisture_Percent`         Soil moisture
  `Fertilizer_kg_per_hectare`     Fertilizer application
  `Irrigation_Hours`              Irrigation duration
  `Pest_Level`                    Pest level
  `Crop_Yield_Tons_per_Hectare`   Crop yield

The missing values are distributed across rainfall, soil moisture, and
fertilizer columns in the current dataset.

------------------------------------------------------------------------

# 🔍 Types of Questions

The Gradio interface is designed for natural-language questions.

### Regional Questions

``` text
How much crop yield is there in Tamil Nadu?

Which region has the highest average crop yield?

Which region has the lowest average crop yield?

Compare Tamil Nadu and Punjab.
```

### Crop Questions

``` text
Which crop has the highest average yield?

What is the average yield of Rice?

Which crop performs best in Tamil Nadu?
```

### Soil Questions

``` text
Which soil type has the highest yield?

Compare Loamy soil and Sandy soil.
```

### Weather Questions

``` text
What is the average rainfall?

How does rainfall relate to crop yield?

Does temperature have a relationship with yield?
```

### Irrigation Questions

``` text
Which irrigation type has the highest average yield?

Compare Rainfed and Drip irrigation.
```

### Fertilizer Questions

``` text
What is the average fertilizer usage?

Does fertilizer usage relate to crop yield?
```

### Data Quality Questions

``` text
Are there missing values?

Which columns have missing values?

How many records are in the dataset?
```

### Advanced Analysis Questions

``` text
What factors are associated with crop yield?

Why is crop yield lower in some regions?

What patterns do you find in the dataset?

Find unusual crop-yield observations.
```

------------------------------------------------------------------------

# 📈 Analysis Capabilities

The current workflow can perform:

### 1. Regional comparison

Average yield can be compared across regions.

### 2. Crop comparison

Crop performance can be analyzed within and across regions.

### 3. Correlation analysis

Relationships between numerical agricultural variables and crop yield
can be examined.

### 4. Soil and climate analysis

The workflow can compare soil and regional conditions.

### 5. Farmer-practice analysis

Irrigation, fertilizer, and pest-related patterns can be examined.

### 6. Anomaly detection

The generated analysis can identify unusually high or low observations.

### 7. Multivariate-style analysis

Multiple numerical factors can be examined together using their
relationships with crop yield.

------------------------------------------------------------------------

# 📊 Visualization

The current visualization layer creates:

``` text
1. Average Crop Yield by Region
2. Rainfall vs Crop Yield
3. Soil Moisture vs Crop Yield
```

Example generated files:

``` text
yield_by_region.png
rainfall_vs_yield.png
soil_moisture_vs_yield.png
```

------------------------------------------------------------------------

# 💡 Example Findings From the Current Demo

For the current synthetic dataset, the analysis identified these
correlations with crop yield:

  Variable             Correlation with Yield
  ------------------ ------------------------
  Rainfall                           0.616351
  Soil Moisture                      0.549129
  Fertilizer                         0.242633
  Irrigation Hours                   0.197776
  Pest Level                        -0.259967
  Temperature                       -0.005554
  Humidity                           0.005917

These are **associations in the demo dataset, not proof of causation**.

The workflow also identified Andhra Pradesh, Karnataka, and Maharashtra
as regions below the overall regional mean in the demonstrated analysis.

------------------------------------------------------------------------

# 🌟 Advantages of AgroDetect AI

## 1. Natural-Language Interaction

Users do not need to write Pandas or Python code.

They can simply ask:

> "What is the average rainfall?"

------------------------------------------------------------------------

## 2. Autonomous Analysis

The system determines what analysis should be performed instead of
requiring the user to specify every analytical step.

------------------------------------------------------------------------

## 3. Autonomous Code Generation

The Coding Agent dynamically generates Python analysis code based on the
investigation plan.

------------------------------------------------------------------------

## 4. Autonomous Error Recovery

If generated code fails, the Debugging Agent can inspect the error,
generate corrected code, and retry within a predefined limit.

------------------------------------------------------------------------

## 5. MCP-Based Tool Access

Agricultural data and analysis operations are exposed as MCP tools,
separating reasoning from tool execution.

------------------------------------------------------------------------

## 6. Explainable Results

The system provides findings, evidence, recommendations, and limitations
instead of returning only a numerical result.

------------------------------------------------------------------------

## 7. Visual Intelligence

The system can automatically generate charts to support data
interpretation.

------------------------------------------------------------------------

## 8. Multiple Question Types

The chatbot can handle questions involving regions, crops, soil,
weather, irrigation, fertilizer, pests, yield, statistics, and
relationships.

------------------------------------------------------------------------

## 9. Reduced Manual Data-Analysis Work

A conventional workflow may require a person to repeatedly write,
execute, debug, and interpret code. AgroDetect AI automates much of that
workflow.

------------------------------------------------------------------------

## 10. Modular Architecture

Each responsibility is separated into an agent or MCP tool, making the
project easier to extend.

------------------------------------------------------------------------

# 🆚 Traditional Analysis vs AgroDetect AI

  Traditional Approach           AgroDetect AI
  ------------------------------ --------------------------------------
  User writes analysis code      Coding Agent generates code
  Manual tool selection          MCP tools provide capabilities
  Manual debugging               Debugging Agent can recover
  Manual chart creation          Visualization Agent creates charts
  Manual interpretation          Root-Cause Agent interprets patterns
  Manual report writing          Report Agent creates report
  Technical knowledge required   Natural-language questions

------------------------------------------------------------------------

# 🛠️ Technology Stack

``` text
Python
Pandas
NumPy
Scikit-learn
Matplotlib
Groq
LangChain
LangGraph
MCP
Gradio
Google Colab
```

### Roles

  Technology     Role
  -------------- ---------------------------------------------
  Groq           LLM reasoning and code generation
  LangChain      LLM/application integration
  LangGraph      Stateful multi-agent workflow orchestration
  MCP            Tool/data access layer
  Pandas         Data analysis
  NumPy          Numerical operations
  Scikit-learn   Data/ML utilities
  Matplotlib     Visualization
  Gradio         Chatbot interface
  Google Colab   Development environment

------------------------------------------------------------------------

# 🚀 Installation

Run in Google Colab:

``` bash
!pip install -q -U \
    langchain \
    langgraph \
    langchain-groq \
    "mcp[cli]" \
    pandas \
    numpy \
    scikit-learn \
    matplotlib \
    gradio
```

------------------------------------------------------------------------

# 🔑 Groq API Configuration

Store your API key in Google Colab Secrets:

``` text
GROQ_API_KEY
```

Then:

``` python
from google.colab import userdata

GROQ_API_KEY = userdata.get("GROQ_API_KEY")

os.environ["GROQ_API_KEY"] = GROQ_API_KEY
```

The project initializes the Groq model through LangChain.

------------------------------------------------------------------------

# 📁 Project Structure

``` text
AgroDetect-AI/
│
├── AgroDetect_AI.ipynb
│
├── agricultural.csv
│
├── yield_by_region.png
├── rainfall_vs_yield.png
├── soil_moisture_vs_yield.png
│
└── README.md
```



# 💬 Example End-to-End Interaction

### User

``` text
Why is crop yield lower in some regions?
```

### AgroDetect AI

``` text
Planner
    ↓
Data Analyst
    ↓
Coding Agent
    ↓
MCP Execution
    ↓
Root-Cause Analysis
    ↓
Visualization
    ↓
Report
```

The final response contains:

-   Key findings
-   Potential contributing factors
-   Evidence
-   Recommendations
-   Limitations

------------------------------------------------------------------------


# 🎓 Project Value

AgroDetect AI demonstrates the integration of several modern AI concepts
in one practical application:

``` text
LLM
 +
Tool Use
 +
MCP
 +
Multi-Agent AI
 +
LangGraph
 +
Autonomous Code Generation
 +
Autonomous Debugging
 +
Data Analysis
 +
Visualization
 +
Natural-Language Interface
```

The project is therefore more than a conventional agricultural
prediction model. Its main contribution is the **autonomous analytical
workflow**.

------------------------------------------------------------------------

# 🏆 Key Project Highlight

> **AgroDetect AI transforms a natural-language agricultural question
> into an autonomous data-analysis workflow. It plans the investigation,
> accesses data through MCP, generates and executes analytical code, can
> recover from coding failures through controlled retries, investigates
> potential contributing factors, creates visualizations, and produces
> an explainable final report.**

------------------------------------------------------------------------

# 👨‍💻 Project

**Project Name:** AgroDetect AI

**Category:** Agentic AI / Autonomous Data Analytics

**Domain:** Agriculture

**Interface:** Gradio

**LLM:** Groq

**Orchestration:** LangGraph

**LLM Framework:** LangChain

**Tool Protocol:** MCP

**Development:** Google Colab

------------------------------------------------------------------------
