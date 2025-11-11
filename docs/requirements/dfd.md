# Data Flow Diagram (DFD)

The Data Flow Diagram illustrates how data moves within the **SkillCheck – Enclosed Access Online Test Platform**.<br>
It represents the logical flow of information between the main actors (**Admin**, **Test Creator**, and **Test Taker**) and the system processes.<br>
All actions ultimately interact with a single centralized **database**, which stores user, test, assignment, and result data.<br>

```mermaid 
---
config:
  layout: elk
---
flowchart TB
    A["Admin"] -- login / manage users --> AUTH["Auth & Roles"]
    C["Creator"] -- login / create tests --> AUTH
    T["Taker"] -- login / start test --> AUTH
    AUTH -- access granted --> A & C & T
    A -- manage --> UM[("Users")]
    C -- create / edit --> TM["Test Management"]
    TM -- store tests --> TS[("Tests")]
    TM -- store questions --> QN[("Questions")]
    C -- assign / publish --> AS["Assignments"]
    AS -- update status / notify --> TS
    AS -- link users --> UM
    T -- attempt / submit --> ATT["Test Attempts"]
    ATT -- save attempt --> ATTEMPTS[("Attempts")]
    ATT -- save responses --> RESPONSES[("Responses")]
    A -- view stats --> RESULTS["Results & Dashboard"]
    C -- view results --> RESULTS
    T -- view own results --> RESULTS
    RESULTS -- fetch test & attempt data --> TS
    RESULTS -- fetch responses --> RESPONSES
     AUTH:::proc
     UM:::store
     TM:::proc
     TS:::store
     QN:::store
     AS:::proc
     ATT:::proc
     ATTEMPTS:::store
     RESPONSES:::store
     RESULTS:::proc

```