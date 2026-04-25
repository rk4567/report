# Data Flow Diagrams (DFDs) - TaskBit Project

## DFD Level 0 (Context Diagram)

```mermaid
graph TB
    User["👤 User"]
    TaskBit["📊 TaskBit System"]
    GitHub["🐙 GitHub"]
    Clerk["🔐 Clerk Auth"]
    Email["📧 Email Service"]
    
    User -->|Login/Register| Clerk
    Clerk -->|Auth Token| User
    User -->|Manage Projects & Tasks| TaskBit
    TaskBit -->|Display Data| User
    TaskBit -->|Integrate| GitHub
    GitHub -->|Webhook Events| TaskBit
    TaskBit -->|Send Notifications| Email
    Email -->|Emails| User
```

---

## DFD Level 1 (Main Processes & Data Stores)

```mermaid
graph TB
    User["👤 User"]
    
    subgraph Processes["🔄 Main Processes"]
        Auth["1.0 User Authentication"]
        WS["2.0 Workspace Management"]
        PROJ["3.0 Project Management"]
        TASK["4.0 Task Management"]
        CMT["5.0 Comment Management"]
        GH["6.0 GitHub Integration"]
    end
    
    subgraph DataStores["💾 Data Stores"]
        DB1["D1: Users"]
        DB2["D2: Workspaces"]
        DB3["D3: Projects"]
        DB4["D4: Tasks"]
        DB5["D5: Comments"]
        DB6["D6: GitHub Integration"]
    end
    
    subgraph External["🔌 External Systems"]
        Clerk["Clerk Auth"]
        GitHub["GitHub API"]
        Inngest["Inngest Events"]
        Email["Email Service"]
    end
    
    User -->|Login| Auth
    Auth -->|Verify| Clerk
    Auth -->|Store/Retrieve| DB1
    
    User -->|Create/Update| WS
    WS -->|Manage Members| DB2
    WS -->|Access Projects| PROJ
    
    PROJ -->|Store/Retrieve| DB3
    PROJ -->|Create Tasks| TASK
    PROJ -->|GitHub Sync| GH
    
    TASK -->|Store/Retrieve| DB4
    TASK -->|Add Comments| CMT
    TASK -->|Sync with GitHub| GH
    
    CMT -->|Store/Retrieve| DB5
    CMT -->|Notify| User
    
    GH -->|OAuth| GitHub
    GH -->|Store Config| DB6
    GitHub -->|Webhooks| GH
    
    Auth -->|Trigger Events| Inngest
    PROJ -->|Trigger Events| Inngest
    TASK -->|Trigger Events| Inngest
    Inngest -->|Send Notifications| Email
```

---

## DFD Level 2 - User Authentication & Profile (Process 1.0)

```mermaid
graph TB
    User["👤 User"]
    
    subgraph AuthProcess["1.0 User Authentication & Profile"]
        Login["1.1 Login/Register"]
        SignUp["1.2 User Signup"]
        Profile["1.3 Profile Setup"]
        Validate["1.4 Validate Credentials"]
    end
    
    subgraph Stores["💾 Data Stores"]
        UserDB["D1: Users"]
        MetadataDB["D1.1: User Metadata"]
    end
    
    Clerk["🔐 Clerk Auth Service"]
    
    User -->|Credentials| Login
    Login -->|Verify| Validate
    Validate -->|Query| UserDB
    Validate -->|Token| Clerk
    Clerk -->|Authenticated| Login
    
    User -->|Email/Password| SignUp
    SignUp -->|Create Account| UserDB
    SignUp -->|Request Profile| Profile
    
    User -->|Profile Info| Profile
    Profile -->|Designation, Department, About| MetadataDB
    Profile -->|Sync| Clerk
    
    Login -->|Session| User
    UserDB -->|User Data| Profile
```

---

## DFD Level 2 - Workspace Management (Process 2.0)

```mermaid
graph TB
    User["👤 User"]
    
    subgraph WorkspaceProcess["2.0 Workspace Management"]
        Create["2.1 Create Workspace"]
        List["2.2 List Workspaces"]
        Update["2.3 Update Workspace"]
        Member["2.4 Manage Members"]
    end
    
    subgraph Stores["💾 Data Stores"]
        WS_DB["D2: Workspaces"]
        WSM_DB["D2.1: Workspace Members"]
        UserDB["D1: Users"]
    end
    
    Email["📧 Email Service"]
    
    User -->|Create| Create
    Create -->|Validate Owner| UserDB
    Create -->|Store| WS_DB
    
    User -->|Get| List
    List -->|Query All| WS_DB
    List -->|Display| User
    
    User -->|Update Info| Update
    Update -->|Modify| WS_DB
    Update -->|Return| User
    
    User -->|Add/Remove| Member
    Member -->|Update| WSM_DB
    Member -->|Query| UserDB
    Member -->|Invite| Email
    Member -->|Notify| User
    
    WS_DB -->|Workspace Data| List
    WS_DB -->|Workspace Data| Update
    WSM_DB -->|Member List| Member
```

---

## DFD Level 2 - Project Management (Process 3.0)

```mermaid
graph TB
    User["👤 User"]
    
    subgraph ProjectProcess["3.0 Project Management"]
        Create["3.1 Create Project"]
        List["3.2 List Projects"]
        Update["3.3 Update Project"]
        Members["3.4 Manage Members"]
        Analytics["3.5 Project Analytics"]
    end
    
    subgraph Stores["💾 Data Stores"]
        Proj_DB["D3: Projects"]
        ProjMem_DB["D3.1: Project Members"]
        Task_DB["D4: Tasks"]
        UserDB["D1: Users"]
    end
    
    Workspace["2.0 Workspace Management"]
    TaskMgmt["4.0 Task Management"]
    
    User -->|Create| Create
    Create -->|Validate Workspace| Workspace
    Create -->|Store| Proj_DB
    
    User -->|Get| List
    List -->|Query by Workspace| Proj_DB
    List -->|Display| User
    
    User -->|Update| Update
    Update -->|Modify| Proj_DB
    Update -->|Return| User
    
    User -->|Add/Remove| Members
    Members -->|Update| ProjMem_DB
    Members -->|Query| UserDB
    Members -->|Notify| User
    
    User -->|View Analytics| Analytics
    Analytics -->|Query Tasks| Task_DB
    Analytics -->|Calculate Stats| Analytics
    Analytics -->|Display| User
    
    Proj_DB -->|Project Data| List
    Proj_DB -->|Task Count| Analytics
    Task_DB -->|Task Data| Analytics
```

---

## DFD Level 2 - Task Management (Process 4.0)

```mermaid
graph TB
    User["👤 User"]
    
    subgraph TaskProcess["4.0 Task Management"]
        Create["4.1 Create Task"]
        List["4.2 List Tasks"]
        Update["4.3 Update Task"]
        Assign["4.4 Assign Task"]
        Filter["4.5 Filter & Sort"]
    end
    
    subgraph Stores["💾 Data Stores"]
        Task_DB["D4: Tasks"]
        UserDB["D1: Users"]
        Proj_DB["D3: Projects"]
    end
    
    ProjectMgmt["3.0 Project Management"]
    CommentMgmt["5.0 Comment Management"]
    GitHub["6.0 GitHub Integration"]
    Inngest["⚡ Inngest Events"]
    
    User -->|Create| Create
    Create -->|Validate| ProjectMgmt
    Create -->|Check Assignee| UserDB
    Create -->|Store| Task_DB
    Create -->|Trigger Event| Inngest
    
    User -->|Get| List
    List -->|Query| Task_DB
    List -->|Display| User
    
    User -->|Update Status/Details| Update
    Update -->|Modify| Task_DB
    Update -->|Trigger Event| Inngest
    Update -->|Sync| GitHub
    Update -->|Return| User
    
    User -->|Assign| Assign
    Assign -->|Verify User| UserDB
    Assign -->|Update| Task_DB
    Assign -->|Notify Assignee| User
    
    User -->|Filter| Filter
    Filter -->|Query with Criteria| Task_DB
    Filter -->|Display| User
    
    Task_DB -->|Task Data| List
    Task_DB -->|Task Data| CommentMgmt
    Task_DB -->|GitHub Issue Link| GitHub
```

---

## DFD Level 2 - Comment Management (Process 5.0)

```mermaid
graph TB
    User["👤 User"]
    
    subgraph CommentProcess["5.0 Comment Management"]
        Create["5.1 Create Comment"]
        List["5.2 List Comments"]
        Delete["5.3 Delete Comment"]
        Notify["5.4 Notify Users"]
    end
    
    subgraph Stores["💾 Data Stores"]
        Comment_DB["D5: Comments"]
        Task_DB["D4: Tasks"]
        UserDB["D1: Users"]
    end
    
    TaskMgmt["4.0 Task Management"]
    Email["📧 Email Service"]
    Inngest["⚡ Inngest Events"]
    
    User -->|Add Comment| Create
    Create -->|Validate Task| Task_DB
    Create -->|Verify User| UserDB
    Create -->|Store| Comment_DB
    Create -->|Trigger Event| Inngest
    
    User -->|Get Comments| List
    List -->|Query by Task| Comment_DB
    List -->|Get User Info| UserDB
    List -->|Display| User
    
    User -->|Delete| Delete
    Delete -->|Verify Ownership| Comment_DB
    Delete -->|Remove| Comment_DB
    Delete -->|Trigger Event| Inngest
    
    Inngest -->|Comment Event| Notify
    Notify -->|Get Task Assignee| Task_DB
    Notify -->|Get User Email| UserDB
    Notify -->|Send| Email
    Notify -->|Update| User
    
    Comment_DB -->|Comment List| List
    Task_DB -->|Task Info| Create
```

---

## DFD Level 2 - GitHub Integration (Process 6.0)

```mermaid
graph TB
    User["👤 User"]
    
    subgraph GitHubProcess["6.0 GitHub Integration"]
        OAuth["6.1 OAuth Authentication"]
        Connect["6.2 Connect Repository"]
        Sync["6.3 Sync Issues"]
        Webhook["6.4 Handle Webhook"]
        CreateIssue["6.5 Create Issue"]
    end
    
    subgraph Stores["💾 Data Stores"]
        GitHub_DB["D6: GitHub Integration"]
        Task_DB["D4: Tasks"]
        Proj_DB["D3: Projects"]
        OAuth_DB["D6.1: OAuth States"]
    end
    
    GitHub["🐙 GitHub API"]
    TaskMgmt["4.0 Task Management"]
    
    User -->|Start OAuth| OAuth
    OAuth -->|Generate State| OAuth_DB
    OAuth -->|Redirect| GitHub
    GitHub -->|Code| OAuth
    OAuth -->|Exchange Token| GitHub
    GitHub -->|Access Token| OAuth
    OAuth -->|Store Config| GitHub_DB
    
    User -->|Select Repo| Connect
    Connect -->|Query| GitHub
    GitHub -->|Repo Data| Connect
    Connect -->|Store| GitHub_DB
    Connect -->|Return| User
    
    User -->|Sync Issues| Sync
    Sync -->|Query| GitHub
    GitHub -->|Issues List| Sync
    Sync -->|Create/Update Tasks| Task_DB
    Sync -->|Return Status| User
    
    GitHub -->|Push Event| Webhook
    Webhook -->|Verify Secret| GitHub_DB
    Webhook -->|Parse Event| Webhook
    Webhook -->|Update Task| Task_DB
    Webhook -->|Update Task Status| TaskMgmt
    
    User -->|Create on GitHub| CreateIssue
    CreateIssue -->|Query Task| Task_DB
    CreateIssue -->|Create Issue| GitHub
    GitHub -->|Issue URL| CreateIssue
    CreateIssue -->|Store URL| Task_DB
    CreateIssue -->|Return| User
    
    GitHub_DB -->|Auth Token| Sync
    GitHub_DB -->|Auth Token| CreateIssue
```

---

## DFD Level 3 - Create Task (Detailed - Process 4.1)

```mermaid
graph TB
    User["👤 User"]
    
    subgraph CreateTaskDetailed["4.1 Create Task - Detailed Flow"]
        Validate["4.1.1 Validate Input"]
        CheckProject["4.1.2 Check Project Access"]
        CheckAssignee["4.1.3 Verify Assignee"]
        GenerateID["4.1.4 Generate Task ID"]
        Store["4.1.5 Store in DB"]
        TriggerEvent["4.1.6 Trigger Event"]
        Response["4.1.7 Send Response"]
    end
    
    subgraph DataAccess["💾 Data Access"]
        Proj_DB["D3: Projects"]
        ProjMem_DB["D3.1: Project Members"]
        Task_DB["D4: Tasks"]
        UserDB["D1: Users"]
    end
    
    Inngest["⚡ Inngest Events"]
    GitHub["6.0 GitHub Integration"]
    
    User -->|Title, Description, etc| Validate
    Validate -->|Verify Fields| Validate
    Validate -->|Check Not Empty| Validate
    
    Validate -->|Yes - Continue| CheckProject
    Validate -->|No - Error| Response
    
    CheckProject -->|Query Project| Proj_DB
    CheckProject -->|Query Members| ProjMem_DB
    Proj_DB -->|Project Exists?| CheckProject
    ProjMem_DB -->|User is Member?| CheckProject
    
    CheckProject -->|Yes - Continue| CheckAssignee
    CheckProject -->|No - Unauthorized| Response
    
    CheckAssignee -->|Query User| UserDB
    CheckAssignee -->|In Project?| ProjMem_DB
    UserDB -->|User Exists?| CheckAssignee
    
    CheckAssignee -->|Yes - Continue| GenerateID
    CheckAssignee -->|No - Invalid| Response
    
    GenerateID -->|Create UUID| GenerateID
    GenerateID -->|Create Task Object| Store
    
    Store -->|Insert Record| Task_DB
    Store -->|Success?| TriggerEvent
    Store -->|No - DB Error| Response
    
    TriggerEvent -->|Emit Event| Inngest
    TriggerEvent -->|Check GitHub Link| GitHub
    TriggerEvent -->|Send OK| Response
    
    Response -->|Task ID + Data| User
    Response -->|Error Message| User
```

---

## DFD Level 3 - Update Task Status (Detailed - Process 4.3)

```mermaid
graph TB
    User["👤 User"]
    
    subgraph UpdateTaskDetailed["4.3 Update Task - Detailed Flow"]
        Validate["4.3.1 Validate Task ID"]
        CheckAccess["4.3.2 Check Access Rights"]
        GetCurrent["4.3.3 Get Current State"]
        Validate_New["4.3.4 Validate New State"]
        UpdateDB["4.3.5 Update Database"]
        SyncGitHub["4.3.6 Sync GitHub"]
        TriggerEvent["4.3.7 Trigger Event"]
        Response["4.3.8 Send Response"]
    end
    
    subgraph DataAccess["💾 Data Access"]
        Task_DB["D4: Tasks"]
        Proj_DB["D3: Projects"]
        ProjMem_DB["D3.1: Project Members"]
        GitHub_DB["D6: GitHub Integration"]
    end
    
    Inngest["⚡ Inngest Events"]
    GitHub["🐙 GitHub API"]
    
    User -->|Task ID, New Status| Validate
    Validate -->|Format Check| Validate
    
    Validate -->|Valid| CheckAccess
    Validate -->|Invalid| Response
    
    CheckAccess -->|Query Task| Task_DB
    CheckAccess -->|Get Project| Proj_DB
    CheckAccess -->|Check Membership| ProjMem_DB
    
    CheckAccess -->|Authorized| GetCurrent
    CheckAccess -->|Unauthorized| Response
    
    GetCurrent -->|Query Task| Task_DB
    Task_DB -->|Return Task Data| GetCurrent
    
    GetCurrent -->|Return Current| Validate_New
    Validate_New -->|Check Status Valid| Validate_New
    Validate_New -->|Check Transition| Validate_New
    
    Validate_New -->|Valid| UpdateDB
    Validate_New -->|Invalid| Response
    
    UpdateDB -->|Update Status| Task_DB
    UpdateDB -->|Success?| SyncGitHub
    UpdateDB -->|No - Error| Response
    
    SyncGitHub -->|Has GitHub Link?| GitHub_DB
    GitHub_DB -->|Get Token| SyncGitHub
    SyncGitHub -->|Update GitHub Issue| GitHub
    GitHub -->|Confirm| SyncGitHub
    
    SyncGitHub -->|Emit Event| TriggerEvent
    TriggerEvent -->|Inngest| Inngest
    TriggerEvent -->|Continue| Response
    
    Response -->|Updated Task| User
    Response -->|Error Message| User
```

---

## DFD Level 3 - GitHub Webhook Processing (Detailed - Process 6.4)

```mermaid
graph TB
    GitHub["🐙 GitHub Webhook"]
    
    subgraph WebhookDetailed["6.4 Handle Webhook - Detailed"]
        Receive["6.4.1 Receive Webhook"]
        Verify["6.4.2 Verify Signature"]
        Parse["6.4.3 Parse Payload"]
        Route["6.4.4 Route Event"]
        UpdateTask["6.4.5 Update Task"]
        Sync_DB["6.4.6 Sync to DB"]
        Response["6.4.7 Send Response"]
    end
    
    subgraph DataAccess["💾 Data Access"]
        GitHub_DB["D6: GitHub Integration"]
        Task_DB["D4: Tasks"]
    end
    
    Inngest["⚡ Inngest Events"]
    
    GitHub -->|Raw Payload| Receive
    Receive -->|X-Hub-Signature| Verify
    
    Verify -->|Query Config| GitHub_DB
    Verify -->|Get Secret| GitHub_DB
    GitHub_DB -->|Secret| Verify
    
    Verify -->|Compute HMAC| Verify
    Verify -->|Match?| Verify
    
    Verify -->|Yes - Valid| Parse
    Verify -->|No - Invalid| Response
    
    Parse -->|Extract Event| Parse
    Parse -->|Extract Action| Parse
    Parse -->|Extract Issue Data| Parse
    
    Parse -->|Issue Event?| Route
    Parse -->|PR Event?| Route
    Parse -->|Push Event?| Route
    
    Route -->|Issue Opened/Closed| UpdateTask
    Route -->|Issue Edited| UpdateTask
    Route -->|Other| Response
    
    UpdateTask -->|Query Task| Task_DB
    UpdateTask -->|GitHub URL Match| Task_DB
    Task_DB -->|Find Task| UpdateTask
    
    UpdateTask -->|Map Status| UpdateTask
    UpdateTask -->|Map Priority| UpdateTask
    
    UpdateTask -->|Update Record| Sync_DB
    Sync_DB -->|Update Task_DB| Task_DB
    
    Sync_DB -->|Emit Event| Inngest
    Inngest -->|Task Updated| Inngest
    
    Inngest -->|OK| Response
    Response -->|200 Success| GitHub
```

---

## DFD Legend

| Symbol | Meaning |
|--------|---------|
| Rounded Box | External System or User |
| Rectangle | Process |
| Cylinder | Data Store |
| Arrow | Data Flow |
| D1, D2, etc | Data Store Reference |

## Key Entities

### Processes
- **1.0**: User Authentication & Profile
- **2.0**: Workspace Management
- **3.0**: Project Management
- **4.0**: Task Management
- **5.0**: Comment Management
- **6.0**: GitHub Integration

### Data Stores
- **D1**: Users (with profile metadata)
- **D2**: Workspaces
- **D3**: Projects & Project Members
- **D4**: Tasks
- **D5**: Comments
- **D6**: GitHub Integration & OAuth States

### External Systems
- **Clerk**: Authentication service
- **GitHub**: Issue tracking & webhooks
- **Inngest**: Event processing
- **Email**: Notification service
- **PostgreSQL**: Main database

## Data Flows Summary

1. **Authentication Flow**: User → Clerk → System
2. **Workspace Flow**: User → Create/Manage Workspaces → Members
3. **Project Flow**: Workspace → Projects → Members → Tasks
4. **Task Flow**: Create → Assign → Update Status → GitHub Sync
5. **Comment Flow**: Task → Comments → Notifications
6. **GitHub Flow**: OAuth → Connect → Webhook Events → Task Updates
