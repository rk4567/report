graph TB
    subgraph "DFD Level 0: Context Diagram"
        User["👤 Users<br/>(Project Managers,<br/>Team Members)"]
        GitHub["🐙 GitHub<br/>API"]
        EmailService["📧 Email<br/>Service"]
        
        TaskBit["<b>TaskBit System</b><br/>Project Management<br/>& Task Tracking"]
        
        User -->|Login, Create Projects,<br/>Manage Tasks| TaskBit
        TaskBit -->|Task Notifications,<br/>Invitations| User
        
        TaskBit -->|OAuth, Webhook Events,<br/>Issue Sync| GitHub
        GitHub -->|Issue Data,<br/>OAuth Tokens| TaskBit
        
        TaskBit -->|Send Emails| EmailService
        EmailService -->|Delivery Status| TaskBit
    end
    
    style TaskBit fill:#61dafb,stroke:#333,stroke-width:3px
    style User fill:#90c53f,color:#fff
    style GitHub fill:#333,color:#fff
    style EmailService fill:#f59e0b,color:#000



graph TB
    subgraph "DFD Level 1: Main Functional Modules"
        subgraph "External Entities"
            User["👤 Users"]
            GitHub["🐙 GitHub"]
            Email["📧 Email"]
        end
        
        subgraph "Core Processes"
            Auth["1. Authentication<br/>(Clerk OAuth)"]
            WS["2. Workspace<br/>Management"]
            Proj["3. Project<br/>Management"]
            Task["4. Task<br/>Management"]
            GH["5. GitHub<br/>Integration"]
            Notif["6. Notifications<br/>(Inngest)"]
            Comments["7. Comments &<br/>Collaboration"]
        end
        
        subgraph "Data Stores"
            DB["🗄️ PostgreSQL<br/>Database"]
            Cache["⚡ Cache<br/>(Task States)"]
            Queue["📋 Job Queue<br/>(Inngest)"]
        end
        
        subgraph "Real-time"
            WS_Server["🔌 WebSocket<br/>Server"]
        end
        
        User -->|Credentials| Auth
        Auth -->|User ID, Token| User
        Auth -->|Verify User| DB
        
        User -->|Create/View<br/>Workspaces| WS
        WS -->|Workspace Data| User
        WS -->|Read/Write| DB
        
        User -->|Manage<br/>Projects| Proj
        Proj -->|Project Data| User
        Proj -->|Read/Write| DB
        Proj -->|Trigger| Notif
        
        User -->|Create/Update<br/>Tasks| Task
        Task -->|Task Data| User
        Task -->|Read/Write| DB
        Task -->|Store State| Cache
        Task -->|Broadcast| WS_Server
        Task -->|Trigger Events| Notif
        Task -->|Link Issues| GH
        
        User -->|Add Comments| Comments
        Comments -->|Comment Data| User
        Comments -->|Read/Write| DB
        Comments -->|Broadcast| WS_Server
        
        GH -->|OAuth Callback| Auth
        GitHub -->|Issue Events| GH
        GH -->|Update Issues| GitHub
        GH -->|Read/Write| DB
        GH -->|Trigger Sync| Notif
        
        Notif -->|Send Task<br/>Assignment| Email
        Notif -->|Queue Tasks| Queue
        Email -->|Delivery ACK| Notif
        
        WS_Server -->|Real-time<br/>Updates| User
        
    end
    
    style Auth fill:#1f3a93,color:#fff
    style WS fill:#3b82f6,color:#fff
    style Proj fill:#0891b2,color:#fff
    style Task fill:#059669,color:#fff
    style GH fill:#333,color:#fff
    style Notif fill:#f59e0b,color:#000
    style Comments fill:#8b5cf6,color:#fff
    style DB fill:#ef4444,color:#fff
    style Queue fill:#f59e0b,color:#000
    style WS_Server fill:#10b981,color:#fff



graph TB
    subgraph "DFD Level 2: GitHub Integration Detailed Flow"
        subgraph "User & Client"
            User["👤 User"]
            Browser["🌐 Browser<br/>(TaskBit UI)"]
        end
        
        subgraph "Frontend Layer"
            OAuth_Init["2.1 OAuth<br/>Initiator"]
            WebhookMonitor["2.2 Webhook<br/>Monitor"]
            RepoSelector["2.3 Repository<br/>Selector"]
        end
        
        subgraph "Backend API Layer"
            AuthHandler["2.4 Auth Flow<br/>Handler"]
            CallbackHandler["2.5 Callback<br/>Handler"]
            WebhookReceiver["2.6 Webhook<br/>Receiver"]
            TokenManager["2.7 Token<br/>Manager"]
        end
        
        subgraph "Data & External"
            GitHub["🐙 GitHub<br/>OAuth Server"]
            GitHubAPI["🐙 GitHub<br/>API"]
            DB["🗄️ Database<br/>(Integration Table)"]
            Queue["📋 Job Queue"]
        end
        
        subgraph "Post-Integration"
            TaskSync["2.8 Task<br/>Sync Engine"]
            NotifEngine["2.9 Notification<br/>Engine"]
        end
        
        User -->|Click Connect| OAuth_Init
        OAuth_Init -->|Generate OAuth URL| Browser
        Browser -->|Redirect to GitHub| GitHub
        
        GitHub -->|Authorization Request| User
        User -->|Grant Permission| GitHub
        
        GitHub -->|Authorization Code| AuthHandler
        AuthHandler -->|Exchange Code| GitHub
        
        GitHub -->|Access Token| CallbackHandler
        CallbackHandler -->|Verify Token| TokenManager
        TokenManager -->|Store Encrypted| DB
        
        TokenManager -->|Return Repos| RepoSelector
        RepoSelector -->|Display List| Browser
        Browser -->|Select Repository| User
        User -->|Confirm| RepoSelector
        
        RepoSelector -->|Create Webhook| WebhookReceiver
        WebhookReceiver -->|POST to GitHub| GitHubAPI
        GitHubAPI -->|Webhook Created| DB
        
        GitHub -->|Issue Event<br/>X-Hub-Signature| WebhookReceiver
        WebhookReceiver -->|Verify Signature| TokenManager
        TokenManager -->|Signature Valid| WebhookReceiver
        
        WebhookReceiver -->|Parse Event| TaskSync
        TaskSync -->|Map Issue State| DB
        TaskSync -->|Issue #45 Closed<br/>→ Task DONE| Queue
        
        Queue -->|Send Email<br/>Notifications| NotifEngine
        NotifEngine -->|Broadcast Update| Browser
        
    end
    
    style OAuth_Init fill:#3b82f6,color:#fff
    style CallbackHandler fill:#3b82f6,color:#fff
    style WebhookReceiver fill:#0891b2,color:#fff
    style AuthHandler fill:#1f3a93,color:#fff
    style TokenManager fill:#059669,color:#fff
    style TaskSync fill:#f59e0b,color:#000
    style NotifEngine fill:#f59e0b,color:#000
    style GitHub fill:#333,color:#fff
    style GitHubAPI fill:#333,color:#fff
    style DB fill:#ef4444,color:#fff
    style Queue fill:#f59e0b,color:#000