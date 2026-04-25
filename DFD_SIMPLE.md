# TaskBit - Simplified DFD Diagrams

## Level 0: Context Diagram

```mermaid
graph LR
    User["👤 User"]
    System["📊 TaskBit System"]
    GitHub["🐙 GitHub"]
    Clerk["🔐 Clerk"]
    Email["📧 Email"]
    
    User <-->|Login/Use| Clerk
    User <-->|Manage Tasks| System
    System <-->|Integrate| GitHub
    System -->|Send Emails| Email
```

---

## Level 1: Main Processes

```mermaid
graph TB
    User["👤 User"]
    
    subgraph Core["Core Processes"]
        Auth["🔐 Authentication"]
        WS["🏢 Workspaces"]
        PROJ["📁 Projects"]
        TASK["✅ Tasks"]
        CMT["💬 Comments"]
        GH["🐙 GitHub"]
    end
    
    subgraph DB["Data Stores"]
        UserDB["Users"]
        WSDB["Workspaces"]
        ProjDB["Projects"]
        TaskDB["Tasks"]
        ComDB["Comments"]
        GhDB["GitHub Config"]
    end
    
    User -->|Login| Auth
    Auth -->|Read/Write| UserDB
    
    User -->|Manage| WS
    WS -->|Read/Write| WSDB
    
    WS -->|Access| PROJ
    PROJ -->|Read/Write| ProjDB
    
    PROJ -->|Create| TASK
    TASK -->|Read/Write| TaskDB
    
    TASK -->|Add| CMT
    CMT -->|Read/Write| ComDB
    
    PROJ -->|Connect| GH
    GH -->|Read/Write| GhDB
```

---

## Level 2: Authentication Process (1.0)

```mermaid
graph LR
    User["👤 User"]
    
    subgraph Auth["Authentication"]
        Login["Login"]
        Verify["Verify"]
        Profile["Profile"]
    end
    
    subgraph Store["Data"]
        UserDB["Users DB"]
        Clerk["Clerk Auth"]
    end
    
    User -->|Email/Pass| Login
    Login -->|Check| Verify
    Verify -->|Query| UserDB
    Verify -->|Token Check| Clerk
    Clerk -->|OK| Profile
    Profile -->|Save Info| UserDB
    UserDB -->|User Data| User
```

---

## Level 2: Workspace Process (2.0)

```mermaid
graph LR
    User["👤 User"]
    
    subgraph Workspace["Workspace"]
        Create["Create"]
        List["List"]
        AddMember["Add Member"]
    end
    
    subgraph Store["Data"]
        WSDB["Workspaces"]
        Members["Members"]
    end
    
    Email["📧 Email"]
    
    User -->|Create| Create
    Create -->|Save| WSDB
    
    User -->|View| List
    List -->|Query| WSDB
    List -->|Display| User
    
    User -->|Invite| AddMember
    AddMember -->|Update| Members
    AddMember -->|Send| Email
```

---

## Level 2: Project Process (3.0)

```mermaid
graph LR
    User["👤 User"]
    
    subgraph Project["Project"]
        Create["Create"]
        List["List"]
        Members["Members"]
        Analytics["Analytics"]
    end
    
    subgraph Store["Data"]
        ProjDB["Projects"]
        MembersDB["Project Members"]
        TaskDB["Tasks"]
    end
    
    User -->|Create| Create
    Create -->|Save| ProjDB
    
    User -->|View| List
    List -->|Query| ProjDB
    List -->|Show| User
    
    User -->|Manage| Members
    Members -->|Update| MembersDB
    
    User -->|View Stats| Analytics
    Analytics -->|Count| TaskDB
    Analytics -->|Display| User
```

---

## Level 2: Task Process (4.0)

```mermaid
graph LR
    User["👤 User"]
    
    subgraph Task["Task"]
        Create["Create"]
        Update["Update"]
        Assign["Assign"]
        List["List"]
    end
    
    subgraph Store["Data"]
        TaskDB["Tasks"]
        UserDB["Users"]
    end
    
    GitHub["GitHub"]
    Events["Events"]
    
    User -->|Create| Create
    Create -->|Save| TaskDB
    Create -->|Trigger| Events
    
    User -->|Change Status| Update
    Update -->|Update| TaskDB
    Update -->|Sync| GitHub
    
    User -->|Assign To| Assign
    Assign -->|Check User| UserDB
    Assign -->|Update| TaskDB
    
    User -->|View| List
    List -->|Query| TaskDB
```

---

## Level 2: Comment Process (5.0)

```mermaid
graph LR
    User["👤 User"]
    
    subgraph Comment["Comment"]
        Add["Add"]
        List["List"]
        Delete["Delete"]
    end
    
    subgraph Store["Data"]
        ComDB["Comments"]
        TaskDB["Tasks"]
    end
    
    Email["📧 Email"]
    
    User -->|Write| Add
    Add -->|Save| ComDB
    Add -->|Get Task| TaskDB
    
    User -->|View| List
    List -->|Query| ComDB
    List -->|Show| User
    
    User -->|Remove| Delete
    Delete -->|Delete| ComDB
    Delete -->|Notify| Email
```

---

## Level 2: GitHub Integration (6.0)

```mermaid
graph LR
    User["👤 User"]
    
    subgraph GitHub_Proc["GitHub"]
        OAuth["OAuth"]
        Connect["Connect Repo"]
        Sync["Sync Issues"]
        Webhook["Webhook"]
    end
    
    subgraph Store["Data"]
        GhDB["GitHub Config"]
        TaskDB["Tasks"]
    end
    
    GitHub["🐙 GitHub API"]
    
    User -->|Login| OAuth
    OAuth -->|Get Token| GitHub
    OAuth -->|Save| GhDB
    
    User -->|Select Repo| Connect
    Connect -->|Query| GitHub
    GitHub -->|Repo Info| Connect
    
    User -->|Sync| Sync
    Sync -->|Get Issues| GitHub
    Sync -->|Create Tasks| TaskDB
    
    GitHub -->|Push Event| Webhook
    Webhook -->|Verify| GhDB
    Webhook -->|Update| TaskDB
```

---

## Level 3: Create Task Detailed (4.1)

```mermaid
graph TD
    User["👤 User<br/>Title, Description,<br/>Assignee, Due Date"]
    
    subgraph Steps["Task Creation Steps"]
        A["1. Validate Input"]
        B["2. Check Project Access"]
        C["3. Verify Assignee"]
        D["4. Create Task ID"]
        E["5. Save to Database"]
        F["6. Trigger Event"]
    end
    
    subgraph DB["Data Access"]
        ProjDB["Projects"]
        UserDB["Users"]
        TaskDB["Tasks"]
    end
    
    A -->|Valid?| B
    B -->|Access OK?| ProjDB
    B -->|Yes| C
    C -->|User Exists?| UserDB
    C -->|Yes| D
    D -->|Generate UUID| E
    E -->|Insert| TaskDB
    E -->|Success| F
    
    User -->|Submit| A
    F -->|Return Task| User
```

---

## Level 3: Update Task Status Detailed (4.3)

```mermaid
graph TD
    User["👤 User<br/>New Status"]
    
    subgraph Steps["Status Update Steps"]
        A["1. Find Task"]
        B["2. Check Access"]
        C["3. Validate State"]
        D["4. Update DB"]
        E["5. Sync GitHub"]
        F["6. Notify Users"]
    end
    
    subgraph DB["Data"]
        TaskDB["Tasks"]
        GhDB["GitHub"]
    end
    
    A -->|Get Task| TaskDB
    B -->|User Authorized?| TaskDB
    B -->|Yes| C
    C -->|Status Valid?| C
    C -->|Yes| D
    D -->|Update| TaskDB
    D -->|Has Link| E
    E -->|Update Issue| GhDB
    E -->|Done| F
    
    User -->|Submit| A
    F -->|OK| User
```

---

## Level 3: GitHub Webhook Processing (6.4)

```mermaid
graph TD
    GitHub["🐙 GitHub<br/>Issue Event"]
    
    subgraph Steps["Webhook Processing"]
        A["1. Receive Webhook"]
        B["2. Verify Signature"]
        C["3. Parse Event"]
        D["4. Find Task"]
        E["5. Update Status"]
        F["6. Send Response"]
    end
    
    subgraph DB["Data"]
        GhDB["GitHub Config"]
        TaskDB["Tasks"]
    end
    
    A -->|Payload| B
    B -->|Get Secret| GhDB
    B -->|Valid?| C
    C -->|Extract Data| D
    D -->|Find by URL| TaskDB
    D -->|Found| E
    E -->|Update| TaskDB
    E -->|Done| F
    
    GitHub -->|Push| A
    F -->|200 OK| GitHub
```

---

## Data Flow: User Creates Task

```mermaid
graph LR
    User["👤 User"]
    Frontend["🖥️ Frontend"]
    API["🔌 API Server"]
    Validation["✓ Validation"]
    Database["💾 Database"]
    Events["⚡ Events"]
    Notification["📧 Notify"]
    
    User -->|Form| Frontend
    Frontend -->|POST /tasks| API
    API -->|Check| Validation
    Validation -->|Valid| Database
    Database -->|Save| Database
    Database -->|Emit| Events
    Events -->|Send Email| Notification
    Notification -->|Success| User
```

---

## Data Flow: GitHub Updates Task

```mermaid
graph LR
    GitHub["🐙 GitHub"]
    Webhook["🔌 Webhook"]
    Verify["✓ Verify"]
    Update["🔄 Update"]
    Database["💾 Database"]
    Cache["⚡ Cache"]
    User["👤 User"]
    
    GitHub -->|Issue Event| Webhook
    Webhook -->|Check| Verify
    Verify -->|OK| Update
    Update -->|Save| Database
    Database -->|Broadcast| Cache
    Cache -->|Realtime| User
```

---

## Complete System Flow

```mermaid
graph TB
    User["👤 User"]
    
    Auth["🔐 Auth<br/>Clerk"]
    WS["🏢 Workspace"]
    PROJ["📁 Project"]
    TASK["✅ Task"]
    CMT["💬 Comment"]
    GH["🐙 GitHub"]
    
    DB[(💾 PostgreSQL)]
    Events["⚡ Events<br/>Inngest"]
    Email["📧 Email"]
    
    User -->|1. Login| Auth
    Auth -->|2. Access| WS
    WS -->|3. Create| PROJ
    PROJ -->|4. Create| TASK
    TASK -->|5. Add| CMT
    TASK -->|6. Sync| GH
    
    Auth -->|Store| DB
    WS -->|Store| DB
    PROJ -->|Store| DB
    TASK -->|Store| DB
    CMT -->|Store| DB
    GH -->|Store| DB
    
    TASK -->|Trigger| Events
    CMT -->|Trigger| Events
    GH -->|Trigger| Events
    
    Events -->|Send| Email
    Email -->|Notify| User
    
    GH -->|Updates| TASK
```

---

## Entity Relationships

```mermaid
graph LR
    User["👤 User"]
    WS["🏢 Workspace"]
    PROJ["📁 Project"]
    TASK["✅ Task"]
    CMT["💬 Comment"]
    GH["🐙 GitHub"]
    
    User -->|Creates| WS
    User -->|Joins| WS
    WS -->|Contains| PROJ
    User -->|Creates| PROJ
    User -->|Joins| PROJ
    PROJ -->|Contains| TASK
    TASK -->|Assigned To| User
    TASK -->|Has| CMT
    CMT -->|Written By| User
    PROJ -->|Integrates| GH
    TASK -->|Links To| GH
```

---

## Legend

```
🔐 = Authentication
🏢 = Workspace Management
📁 = Project Management
✅ = Task Management
💬 = Comments
🐙 = GitHub Integration
💾 = Database
⚡ = Events/Async Processing
📧 = Email/Notification
🖥️ = Frontend
🔌 = API
✓ = Validation
```
