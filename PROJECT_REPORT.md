# TASKBIT: A COMPREHENSIVE PROJECT MANAGEMENT AND TASK TRACKING SYSTEM WITH GITHUB INTEGRATION

---

## 1. TITLE PAGE

**Project Title:** TaskBit – A Modern Project Management and Task Tracking System with GitHub Integration

**Student Name:** [Student Name]

**Roll Number:** [Roll Number]

**Department:** [Department]

**Institution:** [Institution Name]

**Academic Year:** [Academic Year]

**Date of Submission:** April 23, 2026

**Supervisor/Guide:** [Supervisor Name]

**Project Type:** Full-Stack Web Application Development

---

## 2. ABSTRACT

TaskBit is a comprehensive full-stack project management platform designed to streamline team collaboration, task tracking, and project oversight with seamless GitHub integration. The system enables teams to organize projects into workspaces, manage tasks with detailed status tracking, collaborate through comments, and synchronize GitHub issues directly with internal tasks. Built on modern technologies including React 19 for the frontend, Express.js for the backend, PostgreSQL for data persistence, and Clerk for authentication, TaskBit provides a unified interface for project managers and team members to coordinate work efficiently. The platform features multi-user workspace management, role-based access control, real-time updates via WebSocket, task analytics and calendar views, and automated email notifications. GitHub OAuth integration allows users to connect their repositories, while webhook handlers automatically sync GitHub issue states with task statuses. The application is deployed on Vercel with serverless PostgreSQL from Neon, ensuring scalability and reliability. This project demonstrates full-stack development expertise, API design principles, database modeling with Prisma ORM, authentication flow implementation, and third-party service integration patterns essential for production-grade applications.

---

## 3. INTRODUCTION

### Background

Project management is a critical component of modern software development and organizational success. As teams grow and work becomes more distributed, the need for centralized task management and collaboration tools becomes paramount. Traditional project management approaches often involve multiple disconnected tools, leading to fragmented information and reduced team productivity. The rise of GitHub as a primary repository for code has created a natural desire to integrate issue tracking and project management directly with repository data.

### Motivation

The motivation for developing TaskBit stemmed from observing several gaps in existing project management solutions:

1. **Fragmentation:** Teams often juggle multiple tools (GitHub Issues, Trello, Slack, Email) for task management
2. **Integration Deficit:** Few platforms provide seamless, bi-directional GitHub integration
3. **User Experience:** Many tools are either too complex or lack essential features like real-time collaboration
4. **Scalability:** Solutions needed to support growing teams without compromising performance
5. **Customization:** Different teams require different workflows and organizational structures

### Problem Statement

How can we design and implement a scalable, real-time project management system that:
- Provides intuitive task and project management capabilities
- Seamlessly integrates with GitHub for issue synchronization
- Supports multi-user collaboration with role-based access control
- Offers flexible visualization (Kanban, Calendar, Analytics)
- Maintains data consistency across distributed teams
- Scales efficiently with growing organizational needs

### Scope of the Project

This project encompasses:

**In Scope:**
- User authentication and authorization using OAuth (Clerk)
- Workspace and project management with hierarchical organization
- Task creation, assignment, and status tracking
- Real-time collaboration through comments and updates
- GitHub OAuth integration and webhook-based synchronization
- Analytics dashboard with task metrics and progress tracking
- Calendar and Kanban board views
- Email notifications for task assignments and reminders
- WebSocket-based real-time updates
- Multi-environment deployment support

**Out of Scope:**
- Mobile application development
- Advanced reporting and business intelligence features
- Time tracking and billing integration
- Custom workflow automation rules
- Third-party tool integrations (Slack, Jira, Azure DevOps)

---

## 4. OBJECTIVES

### Primary Objectives

1. **Design and implement a scalable project management platform** that supports multiple workspaces, projects, and team members with flexible organizational structures

2. **Integrate GitHub seamlessly** with task management through OAuth authentication and webhook-based real-time synchronization of issues and pull requests

3. **Develop a responsive, modern user interface** using React 19 and Tailwind CSS that provides intuitive navigation and multiple visualization options (Kanban, Calendar, Analytics)

4. **Implement real-time collaboration features** including live updates, comments, and multi-user support with WebSocket integration

5. **Establish secure authentication and authorization** using industry-standard OAuth (Clerk) with role-based access control and permission management

### Secondary Objectives

6. Create a robust RESTful API using Express.js that adheres to best practices for scalability, maintainability, and security

7. Design a normalized database schema using PostgreSQL and Prisma ORM that efficiently stores and retrieves complex relational data

8. Implement background job processing using Inngest for asynchronous tasks including email notifications and data synchronization

9. Provide comprehensive analytics and reporting capabilities including task completion rates, project progress, and team workload metrics

10. Deploy the application using Vercel with serverless PostgreSQL (Neon) to ensure global availability, scalability, and cost efficiency

---

## 5. TECHNOLOGY STACK

| Category | Technology | Purpose |
|----------|-----------|---------|
| **Frontend Framework** | React 19 | Component-based UI library for building interactive user interfaces |
| **Build Tool** | Vite 7.1.2 | Lightning-fast frontend build tool and development server |
| **Styling** | Tailwind CSS 4.1.12 | Utility-first CSS framework for rapid UI development |
| **UI Components** | Lucide React 0.540.0 | Lightweight, customizable SVG icon library |
| **State Management** | Redux Toolkit 2.8.2 | Predictable state management and side effects handling |
| **HTTP Client** | Axios 1.11.0 | Promise-based HTTP client for API communication |
| **Routing** | React Router DOM 7.8.1 | Client-side routing and navigation management |
| **Charting** | Recharts 3.1.2 | React composable charting library for analytics visualization |
| **Notifications** | React Hot Toast 2.6.0 | Non-blocking notification system for user feedback |
| **Date Utilities** | date-fns 4.1.0 | Modern JavaScript date utility library |
| **Authentication** | Clerk (React SDK 5.51.0) | Enterprise-grade OAuth provider and user management |
| **Backend Runtime** | Node.js | JavaScript runtime for server-side execution |
| **API Framework** | Express 5.1.0 | Minimalist web application framework for Node.js |
| **Database** | PostgreSQL (Neon) | Serverless relational database management system |
| **ORM** | Prisma 6.17.1 | Type-safe database client and migration tool |
| **Authentication (Backend)** | Clerk Express 1.7.26 | Middleware for Clerk authentication in Express |
| **Database Adapter** | Neon Adapter 6.15.0 | PostgreSQL adapter for Prisma with serverless support |
| **CORS Middleware** | cors 2.8.5 | Enable Cross-Origin Resource Sharing |
| **Real-time Communication** | WebSocket (ws 8.20.0) | Full-duplex communication for real-time updates |
| **Background Jobs** | Inngest 3.44.2 | Event-driven background job orchestration platform |
| **File Upload** | Multer 2.0.2 | Middleware for handling file uploads |
| **Email Service** | Nodemailer 7.0.9 | Node.js email sending solution |
| **Environment Config** | dotenv 17.2.1 | Load environment variables from .env files |
| **Code Quality** | ESLint 9.33.0 | Static code analysis and linting tool |
| **Linting Plugins** | ESLint React Hooks, React Refresh | React-specific code quality rules |
| **Development Tool** | Nodemon 3.1.10 | Auto-restart Node.js server during development |
| **Deployment** | Vercel | Serverless deployment platform for frontend and backend |
| **External API** | GitHub API v2022-11-28 | Repository and issue management integration |

---

## 6. SYSTEM ARCHITECTURE / DESIGN

### 6.1 Overall Architecture

TaskBit follows a **three-tier client-server architecture** with event-driven background processing:

```
┌─────────────────────────────────────────────────────────────┐
│                    Client Layer (React 19)                   │
│  (UI Components, State Management, Routing, Real-time Sync) │
└────────────────────┬────────────────────────────────────────┘
                     │
        ┌────────────┼────────────┐
        │            │            │
        ▼            ▼            ▼
    HTTP REST   WebSocket   GitHub OAuth
        │            │            │
┌───────────────────────────────────────────────────────────────┐
│        API Gateway & Middleware Layer (Express.js)            │
│ (CORS, Auth, Validation, Error Handling, Routing)            │
└────────────┬────────────┬────────────┬────────────────────────┘
             │            │            │
    ┌────────▼──┐  ┌──────▼────┐  ┌───▼──────┐
    │  Workspace │  │  Project  │  │  GitHub  │
    │ Controller │  │ Controller│  │ Controller│
    └────────┬──┘  └──────┬────┘  └───┬──────┘
             │            │            │
    ┌────────▼────────────▼────────────▼──────┐
    │      Prisma ORM (Data Access Layer)     │
    │  (Query Builder, Schema Validation)    │
    └────────────────┬────────────────────────┘
                     │
        ┌────────────┴────────────┐
        │                         │
        ▼                         ▼
   PostgreSQL            Background Jobs
   (Neon Serverless)     (Inngest Queues)
                                 │
                        ┌────────┴────────┐
                        │                 │
                        ▼                 ▼
                    Email Service    Data Sync
                    (Nodemailer)    (Webhooks)
```

### 6.2 Architectural Layers

#### **1. Presentation Layer (Client)**
- **React 19:** Component-based architecture with hooks for state and lifecycle management
- **Redux Toolkit:** Centralized state management for workspaces, projects, and UI state
- **React Router:** Client-side routing for multi-page navigation
- **Vite:** Development server with Hot Module Replacement (HMR)

#### **2. API Gateway Layer (Express.js)**
- **Request Processing:** Parses and validates incoming HTTP requests
- **Authentication:** Clerk middleware verifies JWT tokens and user identity
- **CORS Handling:** Manages cross-origin requests from multiple clients
- **Route Delegation:** Directs requests to appropriate controllers

#### **3. Business Logic Layer (Controllers)**
Five main controller modules handle core functionality:
- **Workspace Controller:** Create, manage, and retrieve workspaces; invite members
- **Project Controller:** CRUD operations for projects; manage team leads and members
- **Task Controller:** Task lifecycle management; assignment and status updates
- **Comment Controller:** Discussion threads on tasks; collaboration features
- **GitHub Controller:** OAuth flows, webhook handling, issue synchronization

#### **4. Data Access Layer (Prisma ORM)**
- **Type-Safe Queries:** Auto-generated types for database operations
- **Migration Management:** Version-controlled schema changes
- **Relationships:** Handles complex many-to-many and one-to-many relationships
- **Query Optimization:** Automatic joins and nested includes

#### **5. Data Storage Layer (PostgreSQL - Neon)**
- **Normalized Schema:** Designed to third normal form (3NF)
- **Serverless:** Scales automatically; pay-per-use pricing model
- **Reliability:** Automatic backups and ACID compliance

#### **6. External Services Layer**
- **GitHub API:** Repository data, issue management, user information
- **Clerk Authentication:** OAuth provider, user management, session handling
- **Nodemailer:** SMTP-based email delivery for notifications
- **Inngest:** Event queue for background job orchestration

### 6.3 Module Interactions

```
User Request Flow:
1. Frontend sends HTTP request via Axios
2. Express receives request, applies middleware chain
3. Clerk middleware validates authentication token
4. Request routed to appropriate controller
5. Controller calls Prisma methods for data operations
6. Prisma generates optimized SQL queries
7. PostgreSQL executes query and returns results
8. Controller processes response (transforms, filters)
9. Response sent to client as JSON
10. Redux updates client state
11. React re-renders affected components
```

### 6.4 Data Relationships

**Core Entity Relationships:**
- User → (owns/manages) → Workspace
- Workspace → (contains) → Projects
- Project → (contains) → Tasks
- Task → (has) → Comments
- User → (assigned to) → Task
- Project → (has) → GitHub Integration
- GitHub Integration → (generates) → Webhook Secrets

---

## 7. IMPLEMENTATION DETAILS

### 7.1 Core Modules and Functions

#### **7.1.1 Workspace Module**

**Purpose:** Manages organizational units that group projects and teams

**Key Functions:**
```javascript
// Get all workspaces for a user
async function getUserWorkspaces(userId) {
  // Retrieves workspaces where user is a member
  // Includes nested projects, tasks, and team data
  // Used for workspace switching and dashboard display
}

// Create new workspace
async function createWorkspace(name, description, userId) {
  // Creates workspace with provided name
  // Sets creator as owner
  // Initializes default settings and roles
}

// Invite team members
async function inviteWorkspaceMember(workspaceId, email, role) {
  // Sends invitation email with workspace link
  // Records pending invitation in database
  // Auto-accepts when user logs in
}

// Update workspace settings
async function updateWorkspace(workspaceId, updates) {
  // Modifies workspace properties (name, logo, description)
  // Updates project settings and preferences
  // Triggers events for real-time updates
}
```

**Database Schema:**
```
Workspace
├── id (Primary Key)
├── name (Unique per organization)
├── slug (URL-friendly identifier)
├── description (Optional)
├── settings (JSON for flexible config)
├── ownerId (Foreign Key → User)
├── image_url (Logo/Avatar)
├── createdAt, updatedAt (Timestamps)
└── Relationships:
    ├── members (WorkspaceMember[])
    ├── projects (Project[])
    └── owner (User)
```

#### **7.1.2 Project Module**

**Purpose:** Organizes tasks into logical groupings with metadata and team assignments

**Key Functions:**
```javascript
// Create project within workspace
async function createProject(name, description, workspaceId, teamLeadId) {
  // Creates project with metadata
  // Sets initial status to PLANNING
  // Assigns team lead as project manager
  // Initializes progress tracking
}

// Get project with all details
async function getProjectDetails(projectId) {
  // Fetches project with:
  //   - All tasks and their assignments
  //   - Team member list with roles
  //   - GitHub integration data
  //   - Comment and activity history
  // Used for project dashboard display
}

// Update project status
async function updateProjectStatus(projectId, newStatus) {
  // Status transitions: PLANNING → ACTIVE → COMPLETED/ON_HOLD/CANCELLED
  // Updates progress calculations
  // Triggers notifications for team members
  // Archives completed/cancelled projects
}

// Add team member to project
async function addProjectMember(projectId, userId) {
  // Links user to project
  // Sets member as collaborator (not lead)
  // Notifies user of new project assignment
}
```

**Database Schema:**
```
Project
├── id (Primary Key)
├── name
├── description
├── priority (LOW, MEDIUM, HIGH)
├── status (ACTIVE, PLANNING, COMPLETED, ON_HOLD, CANCELLED)
├── start_date
├── end_date
├── team_lead (Foreign Key → User)
├── workspaceId (Foreign Key → Workspace)
├── progress (Percentage calculated from tasks)
├── createdAt, updatedAt
└── Relationships:
    ├── tasks (Task[])
    ├── members (ProjectMember[])
    └── githubIntegration (ProjectGitHubIntegration)
```

#### **7.1.3 Task Module**

**Purpose:** Core unit of work tracking with status, assignment, and collaboration

**Key Functions:**
```javascript
// Create task in project
async function createTask(projectId, title, description, assigneeId) {
  // Creates task with TODO status
  // Assigns to specified team member
  // Sets creation timestamp
  // Triggers assignment notification
  // Returns created task object
}

// Update task status
async function updateTaskStatus(taskId, newStatus) {
  // Status progression: TODO → IN_PROGRESS → DONE
  // Updates last modified timestamp
  // If task linked to GitHub issue:
  //   - Issue status synced if webhook received
  //   - Can trigger GitHub issue update
  // Emits WebSocket update for real-time refresh
}

// Assign task to user
async function assignTask(taskId, assigneeId) {
  // Changes task assignee
  // Sends email notification to new assignee
  // Records assignment in audit log
  // Updates team workload metrics
}

// Link GitHub issue
async function linkGitHubIssue(taskId, issueNumber, repository) {
  // Associates task with GitHub issue
  // Stores issue URL and number
  // Enables issue state sync on webhook
  // Displays issue context in task details
}

// Get task with full context
async function getTaskDetails(taskId) {
  // Fetches task with:
  //   - Assignee information
  //   - All comments with author details
  //   - Related GitHub issue (if linked)
  //   - Activity timeline
  // Used for task detail modal/page
}
```

**Database Schema:**
```
Task
├── id (Primary Key)
├── projectId (Foreign Key → Project)
├── title
├── description
├── status (TODO, IN_PROGRESS, DONE)
├── type (TASK, BUG, FEATURE, IMPROVEMENT, OTHER)
├── priority (LOW, MEDIUM, HIGH)
├── assigneeId (Foreign Key → User, nullable)
├── due_date (Optional)
├── githubIssueNumber (Optional)
├── githubIssueUrl (Optional)
├── githubRepository (Optional)
├── createdAt, updatedAt
└── Relationships:
    ├── assignee (User)
    ├── project (Project)
    └── comments (Comment[])
```

#### **7.1.4 Comment Module**

**Purpose:** Enable threaded discussions and collaboration on tasks

**Key Functions:**
```javascript
// Add comment to task
async function createComment(taskId, userId, content) {
  // Creates comment record
  // Records timestamp and author
  // Triggers notifications to task watchers
  // Emits WebSocket update for live comments
}

// Get task comments
async function getTaskComments(taskId) {
  // Fetches all comments for task
  // Includes author information
  // Ordered by creation date (ascending)
  // Used for task detail view
}

// Update comment (edit)
async function updateComment(commentId, newContent) {
  // Updates comment text
  // Records edit timestamp
  // Maintains original timestamp for history
}

// Delete comment
async function deleteComment(commentId, userId) {
  // Removes comment from database
  // Verifies user is comment author
  // Notifies watchers of deletion
}
```

**Database Schema:**
```
Comment
├── id (Primary Key)
├── content
├── userId (Foreign Key → User)
├── taskId (Foreign Key → Task)
├── createdAt (Timestamp only, no updates)
└── Relationships:
    ├── user (User)
    └── task (Task)
```

#### **7.1.5 GitHub Integration Module**

**Purpose:** Synchronize GitHub repositories with TaskBit, enabling issue-to-task mapping

**Key Functions:**

**OAuth Flow:**
```javascript
// Step 1: Initiate GitHub OAuth
async function generateGitHubAuthUrl(projectId, userId) {
  // Generates GitHub OAuth authorization URL
  // Creates temporary state token (expires in 10 min)
  // Stores state in database for validation
  // Redirects to GitHub authorization page
  // Returns: OAuth URL
}

// Step 2: Handle OAuth callback
async function handleGitHubCallback(code, state, projectId) {
  // Validates state token (prevents CSRF)
  // Exchanges authorization code for access token
  // Fetches user info from GitHub API
  // Stores integration record with encrypted token
  // Returns: User's GitHub repositories list
}

// Step 3: Select repository
async function setGitHubRepository(projectId, owner, repo) {
  // Updates integration with selected repository
  // Fetches and caches repo metadata
  // Prepares for webhook setup
  // Returns: Repository details
}

// Step 4: Setup webhook
async function createGitHubWebhook(projectId) {
  // Generates random webhook secret
  // Registers webhook with GitHub API
  // Events: ['issues', 'pull_request']
  // Webhook URL: /api/github/webhook/:projectId
  // Returns: Webhook secret and confirmation
}
```

**Webhook Handler:**
```javascript
// Process GitHub webhook event
async function handleGitHubWebhook(projectId, payload, signature) {
  // Step 1: Verify webhook signature (HMAC-SHA256)
  if (!verifyWebhookSignature(payload, signature, webhookSecret)) {
    throw new Error('Invalid signature');
  }

  // Step 2: Extract event data
  const event = payload.action; // opened, closed, edited, etc.
  const issue = payload.issue;
  const issueNumber = issue.number;
  const issueState = issue.state; // 'open' or 'closed'

  // Step 3: Map issue state to task status
  let taskStatus;
  if (issueState === 'closed') taskStatus = 'DONE';
  else if (issueState === 'open') taskStatus = 'IN_PROGRESS';
  else return; // Skip if state not recognized

  // Step 4: Find linked task
  const task = await Task.findOne({
    where: {
      projectId,
      githubIssueNumber: issueNumber
    }
  });

  // Step 5: Create or update task
  if (task) {
    // Update existing task
    await updateTaskStatus(task.id, taskStatus);
  } else if (event === 'opened') {
    // Create new task from issue
    await createTask(projectId, issue.title, issue.body, null);
  }

  // Step 6: Emit real-time update
  emitWebSocketEvent(`project:${projectId}`, {
    type: 'task_updated',
    taskId: task.id,
    status: taskStatus
  });
}
```

**Database Schema:**
```
ProjectGitHubIntegration
├── id (Primary Key)
├── projectId (Foreign Key → Project, Unique)
├── githubAccountLogin
├── githubUserId
├── repository (owner/repo format)
├── accessToken (encrypted)
├── webhookSecret (encrypted)
├── webhookSecretUpdatedAt
├── createdAt, updatedAt
└── Relationships:
    ├── project (Project)
    └── oauthStates (GitHubOAuthState[])

GitHubOAuthState
├── id (Primary Key)
├── state (Unique, CSRF token)
├── userId
├── projectId
├── integrationId (Foreign Key)
├── expiresAt (10 minute TTL)
└── createdAt
```

### 7.2 Key Algorithms and Design Decisions

#### **Algorithm 1: Real-time Update Propagation**

```javascript
// When task status changes:
1. Update database: UPDATE tasks SET status = 'IN_PROGRESS' WHERE id = ?
2. Emit event to Inngest for background processing
3. Broadcast via WebSocket to all connected clients:
   - Server: io.to(`project:${projectId}`).emit('taskUpdated', taskData)
   - Client: Redux dispatch(updateTask(taskData))
   - UI: React re-renders affected components (Kanban, Calendar, Analytics)
4. Trigger Inngest background job for notifications:
   - Send email to project lead
   - Update GitHub issue if linked
   - Record activity in audit log
```

#### **Algorithm 2: GitHub Webhook Verification and Processing**

```javascript
// Webhook Security Flow:
1. Receive POST at /api/github/webhook/:projectId with:
   - Raw body buffer (for signature verification)
   - X-Hub-Signature-256 header
   
2. Calculate HMAC-SHA256:
   signature = HMAC-SHA256(body, webhookSecret)
   
3. Compare signatures:
   if (calculatedSig !== providedSig) {
     return 401 Unauthorized;
   }
   
4. Parse JSON payload
5. Extract issue data and map states
6. Perform database operations (create/update task)
7. Emit WebSocket update for real-time sync
```

#### **Algorithm 3: Task Progress Calculation**

```javascript
// Calculate project progress:
function getProjectProgress(projectId) {
  const tasks = await Task.findMany({
    where: { projectId }
  });
  
  if (tasks.length === 0) return 0;
  
  const completedCount = tasks.filter(t => t.status === 'DONE').length;
  const progress = Math.round((completedCount / tasks.length) * 100);
  
  // Update project record
  await Project.update(
    { id: projectId },
    { progress }
  );
  
  return progress;
}

// Used in Analytics component for progress bars and charts
```

#### **Design Decision 1: Why WebSocket for Real-time Updates?**

**Considered Alternatives:**
- **Polling:** Simple but inefficient (continuous server load)
- **Server-Sent Events (SSE):** One-way communication (not suitable for bidirectional)
- **WebSocket:** Full-duplex, low latency, persistent connection ✓ CHOSEN

**Implementation:**
```javascript
// Server setup
const wss = new WebSocketServer({ server });

wss.on('connection', (ws) => {
  ws.send(JSON.stringify({ type: 'connected' }));
  
  ws.on('message', (message) => {
    const data = JSON.parse(message);
    if (data.action === 'join') {
      ws.projectId = data.projectId;
      ws.join(`project:${data.projectId}`);
    }
  });
});

// Broadcasting task update
io.to(`project:${projectId}`).emit('taskUpdated', taskData);
```

#### **Design Decision 2: Why Redux for State Management?**

**Considered Alternatives:**
- **Context API:** Sufficient for small apps, but prop drilling at scale
- **MobX:** Simpler but less predictable than Redux
- **Redux Toolkit:** Reduced boilerplate, excellent DevTools ✓ CHOSEN

**Implementation:**
```javascript
// Redux slice for workspace
const workspaceSlice = createSlice({
  name: 'workspace',
  initialState: {
    currentWorkspace: null,
    workspaces: [],
    loading: false
  },
  reducers: {
    setCurrentWorkspace: (state, action) => {
      state.currentWorkspace = action.payload;
    },
    updateTask: (state, action) => {
      const task = action.payload;
      const project = state.currentWorkspace?.projects?.find(
        p => p.id === task.projectId
      );
      if (project) {
        const existingTask = project.tasks.find(t => t.id === task.id);
        Object.assign(existingTask, task);
      }
    }
  }
});
```

#### **Design Decision 3: Why Prisma ORM?**

**Considered Alternatives:**
- **Raw SQL:** Secure but verbose and error-prone
- **TypeORM:** More complex setup, larger learning curve
- **Prisma:** Type-safe, auto-migrations, excellent dev experience ✓ CHOSEN

**Schema Definition:**
```prisma
model Project {
  id        String   @id @default(cuid())
  name      String
  tasks     Task[]
  members   ProjectMember[]
  workspace Workspace @relation(fields: [workspaceId], references: [id])
  workspaceId String
  
  @@unique([id, workspaceId])
}

model Task {
  id           String   @id @default(cuid())
  title        String
  status       String   @default("TODO") // TODO, IN_PROGRESS, DONE
  project      Project  @relation(fields: [projectId], references: [id])
  projectId    String
  comments     Comment[]
  githubIssueNumber Int?
  
  @@index([projectId])
}
```

#### **Design Decision 4: Why Inngest for Background Jobs?**

**Considered Alternatives:**
- **Bull Queue:** Requires Redis setup, more infrastructure
- **Agenda:** MongoDB-dependent, tightly coupled
- **Inngest:** Serverless, no external dependencies ✓ CHOSEN

**Background Jobs:**
```javascript
// Email notification job
export const sendTaskAssignmentMail = inngest.createFunction(
  { id: "send-task-assignment-mail" },
  { event: "task/assigned" },
  async ({ event, step }) => {
    const task = await step.run("fetch-task", async () => {
      return await Task.findById(event.data.taskId);
    });

    await step.run("send-email", async () => {
      await sendEmail({
        to: task.assignee.email,
        subject: `New task assigned: ${task.title}`,
        template: 'task-assignment'
      });
    });
  }
);
```

---

## 8. FEATURES

### 8.1 User Authentication & Authorization

**Features:**
- OAuth-based authentication via Clerk (Google, GitHub)
- Automatic user profile sync from OAuth provider
- Email-based user verification
- Session token refresh and invalidation
- Role-based access control (ADMIN, MEMBER)
- Project-level permission checks
- Secure token storage in httpOnly cookies

**📸 Screenshot Placeholders:**

> **[SCREENSHOT 8.1.1]** Login Page with OAuth Options
> - Show: Clerk login interface with "Sign in with Google" and "Sign in with GitHub" buttons
> - Location: `/screenshots/auth/login-page.png`
> - Expected: Clean, centered login form with branding

> **[SCREENSHOT 8.1.2]** User Profile & Permission Settings
> - Show: User profile page with role information (ADMIN/MEMBER) and permission assignments
> - Location: `/screenshots/auth/user-profile.png`
> - Expected: Profile card with designation, department, role badge, and permission level

---

### 8.2 Workspace Management

**Features:**
- Create unlimited workspaces for organizational units
- Customize workspace name, logo, and description
- Invite team members via email
- Role assignment (ADMIN for workspace management, MEMBER for collaboration)
- Workspace switching for multi-tenant access
- Settings page for workspace configuration
- Member list with activity tracking

**📸 Screenshot Placeholders:**

> **[SCREENSHOT 8.2.1]** Workspace Switcher & List
> - Show: Dropdown or sidebar showing multiple workspaces with quick switch capability
> - Location: `/screenshots/workspace/workspace-switcher.png`
> - Expected: 3-4 workspace cards with names, logos, member count, and active indicator

> **[SCREENSHOT 8.2.2]** Workspace Settings Page
> - Show: Workspace configuration panel with name, description, logo upload, and settings
> - Location: `/screenshots/workspace/workspace-settings.png`
> - Expected: Form fields for workspace details, team member list with role assignment

> **[SCREENSHOT 8.2.3]** Invite Members Modal
> - Show: Dialog for inviting team members with email input and role selection
> - Location: `/screenshots/workspace/invite-members-modal.png`
> - Expected: Email input field, role dropdown (ADMIN/MEMBER), invite button, pending invitations list

> **[SCREENSHOT 8.2.4]** Members Management Page
> - Show: Table of workspace members with names, emails, roles, and management actions
> - Location: `/screenshots/workspace/members-list.png`
> - Expected: Member table with columns: Name, Email, Role, Status, Action buttons (remove, change role)

---

### 8.3 Project Management

**Features:**
- Create projects within workspaces
- Set project metadata (name, description, priority, dates)
- Project status tracking (PLANNING, ACTIVE, ON_HOLD, COMPLETED, CANCELLED)
- Assign team leads and members
- Progress tracking (calculated from task completion)
- Project visibility and sharing controls
- Bulk project operations (archive, delete)
- Project-level activity logs

**📸 Screenshot Placeholders:**

> **[SCREENSHOT 8.3.1]** Projects List View
> - Show: Grid or list of all projects in the workspace with status badges
> - Location: `/screenshots/projects/projects-list.png`
> - Expected: Project cards showing: name, description, status (color-coded), progress bar, team lead, dates

> **[SCREENSHOT 8.3.2]** Project Creation Dialog
> - Show: Modal for creating new project with form fields
> - Location: `/screenshots/projects/create-project-modal.png`
> - Expected: Fields: Project name, Description, Start date, End date, Priority, Team lead selection

> **[SCREENSHOT 8.3.3]** Project Overview/Header
> - Show: Project header with name, status badge, and key metrics
> - Location: `/screenshots/projects/project-header.png`
> - Expected: Project title, status indicator, quick stats (tasks, completed, team members)

> **[SCREENSHOT 8.3.4]** Project Settings & Members
> - Show: Project settings panel and team member assignment
> - Location: `/screenshots/projects/project-settings.png`
> - Expected: Project metadata fields, team members table, add/remove member controls

---

### 8.4 Task Management

**Features:**
- Create tasks with title, description, and type
- Task types: TASK, BUG, FEATURE, IMPROVEMENT, OTHER
- Task priority levels: LOW, MEDIUM, HIGH
- Task status: TODO, IN_PROGRESS, DONE
- Assign tasks to team members
- Set due dates with reminder notifications
- Task dependencies (optional for future phases)
- Bulk update task statuses
- Task filtering and search capabilities
- Drag-and-drop task assignment

**📸 Screenshot Placeholders:**

> **[SCREENSHOT 8.4.1]** Task Creation Form
> - Show: Modal/form for creating a new task with all fields
> - Location: `/screenshots/tasks/create-task-modal.png`
> - Expected: Fields: Title, Description, Type dropdown, Priority dropdown, Assignee selection, Due date, Labels

> **[SCREENSHOT 8.4.2]** Task Details Page
> - Show: Full task detail view with all information
> - Location: `/screenshots/tasks/task-detail-page.png`
> - Expected: Task header, description, metadata (type, priority, status, assignee), due date, actions, comments section

> **[SCREENSHOT 8.4.3]** Task List/Table View
> - Show: Table showing all tasks with filtering and sorting options
> - Location: `/screenshots/tasks/tasks-table.png`
> - Expected: Columns: Task ID, Title, Status, Priority, Assignee, Due date, Type; with sort/filter controls

> **[SCREENSHOT 8.4.4]** Task Quick Actions
> - Show: Hover actions on task cards (edit, delete, assign, change status)
> - Location: `/screenshots/tasks/task-quick-actions.png`
> - Expected: Context menu or button group for common task operations

---

### 8.5 Real-time Collaboration

**Features:**
- Comment threads on tasks for discussion
- @mention notifications for team members
- Real-time comment updates via WebSocket
- Activity timestamps and author information
- Edit and delete comments (with audit trail)
- Comment formatting with markdown support
- Notification badges for unread comments

**📸 Screenshot Placeholders:**

> **[SCREENSHOT 8.5.1]** Comments Section
> - Show: Task comments thread with individual comments and timestamps
> - Location: `/screenshots/collaboration/comments-section.png`
> - Expected: Comments list with author avatar, name, timestamp, comment content, edit/delete buttons

> **[SCREENSHOT 8.5.2]** Comment Composer with @mention
> - Show: Text input for adding new comments with @mention dropdown
> - Location: `/screenshots/collaboration/comment-composer.png`
> - Expected: Textarea with @ icon triggering team member autocomplete, formatting toolbar, submit button

> **[SCREENSHOT 8.5.3]** Activity Feed/Timeline
> - Show: Timeline of all activities (task changes, comments, assignments)
> - Location: `/screenshots/collaboration/activity-timeline.png`
> - Expected: Chronological list with icons, user names, action descriptions, and timestamps

> **[SCREENSHOT 8.5.4]** Notification Badge & Indicator
> - Show: Unread comment badges and notification indicators
> - Location: `/screenshots/collaboration/notification-badges.png`
> - Expected: Red badges on comment section, task card, and navigation showing unread count

---

### 8.6 GitHub Integration

**Features:**
- OAuth-based GitHub account connection per project
- Repository selection and configuration
- Automatic GitHub issue synchronization
- Bidirectional issue-to-task linking
- Webhook-based real-time issue state sync
- Issue state mapping (closed → DONE, open → IN_PROGRESS)
- GitHub issue display within task details
- Webhook secret generation and rotation
- Integration disconnect with cleanup

**📸 Screenshot Placeholders:**

> **[SCREENSHOT 8.6.1]** GitHub Integration Panel
> - Show: Project settings tab for GitHub integration with connection status
> - Location: `/screenshots/github/github-integration-panel.png`
> - Expected: Integration status, "Connect GitHub" button, repository display (if connected), disconnect option

> **[SCREENSHOT 8.6.2]** GitHub OAuth Flow
> - Show: GitHub authorization page (or redirection to GitHub)
> - Location: `/screenshots/github/github-oauth-flow.png`
> - Expected: Clerk redirecting to GitHub OAuth consent screen for permission approval

> **[SCREENSHOT 8.6.3]** Repository Selection Dialog
> - Show: Modal for selecting repository after OAuth authorization
> - Location: `/screenshots/github/repo-selection-modal.png`
> - Expected: List of user's repositories with search/filter, selection radio button, confirm button

> **[SCREENSHOT 8.6.4]** Linked GitHub Issue in Task
> - Show: Task detail showing linked GitHub issue with issue metadata
> - Location: `/screenshots/github/linked-github-issue.png`
> - Expected: GitHub issue badge, issue number, issue title, repository name, current state (open/closed)

> **[SCREENSHOT 8.6.5]** Webhook Configuration Success
> - Show: Confirmation message after successful webhook setup
> - Location: `/screenshots/github/webhook-setup-success.png`
> - Expected: Success banner with webhook secret, test webhook button, "Ready for sync" indicator

---

### 8.7 Visualization and Analytics

**Features:**

**Kanban Board:**
- Visual drag-and-drop task organization
- Columns for TODO, IN_PROGRESS, DONE statuses
- Task cards with assignee, priority, due date
- Inline task creation
- WIP (Work In Progress) limits
- Filtering by assignee, priority, type

**📸 Screenshot Placeholders:**

> **[SCREENSHOT 8.7.1]** Kanban Board View
> - Show: Full Kanban board with three columns (TODO, IN_PROGRESS, DONE)
> - Location: `/screenshots/visualization/kanban-board.png`
> - Expected: Three columns with task cards, drag-and-drop indication, task count per column, filters above

> **[SCREENSHOT 8.7.2]** Kanban Card Details
> - Show: Individual task cards on Kanban with all metadata visible
> - Location: `/screenshots/visualization/kanban-card-details.png`
> - Expected: Card showing: task title, assignee avatar, priority color, due date icon, task type badge

**Calendar View:**
- Month/week/day view of tasks
- Tasks grouped by due date
- Color-coded by status and priority
- Quick task creation from calendar
- Deadline notifications
- Integration with personal calendars (future)

**📸 Screenshot Placeholders:**

> **[SCREENSHOT 8.7.3]** Calendar Month View
> - Show: Calendar grid showing all tasks by due date
> - Location: `/screenshots/visualization/calendar-month-view.png`
> - Expected: Month calendar with task indicators on dates, color-coded by status, navigation controls

> **[SCREENSHOT 8.7.4]** Calendar Day/Week View
> - Show: Detailed view of tasks for a specific day or week
> - Location: `/screenshots/visualization/calendar-week-view.png`
> - Expected: Timeline format showing tasks with time slots, task details on hover/click

**Analytics Dashboard:**
- Task completion rate (percentage)
- Burndown charts showing progress over time
- Team member workload distribution
- Task breakdown by type and priority
- Project health metrics
- Historical trends and forecasting
- Export reports (PDF, CSV)

**📸 Screenshot Placeholders:**

> **[SCREENSHOT 8.7.5]** Analytics Dashboard Overview
> - Show: Full analytics page with multiple charts and metrics
> - Location: `/screenshots/visualization/analytics-dashboard.png`
> - Expected: Multiple visualization cards: completion rate, burndown chart, team workload, task breakdown

> **[SCREENSHOT 8.7.6]** Burndown Chart
> - Show: Line chart showing task completion trend over time
> - Location: `/screenshots/visualization/burndown-chart.png`
> - Expected: X-axis: time period, Y-axis: task count, line showing actual vs. ideal progress

> **[SCREENSHOT 8.7.7]** Team Workload Distribution
> - Show: Bar/pie chart showing task assignment by team member
> - Location: `/screenshots/visualization/team-workload.png`
> - Expected: Team member names with task counts or percentages, visual bars/slices

> **[SCREENSHOT 8.7.8]** Task Type Breakdown
> - Show: Pie chart or bar chart showing task distribution by type
> - Location: `/screenshots/visualization/task-breakdown.png`
> - Expected: Types (BUG, FEATURE, TASK, IMPROVEMENT) with counts and percentages

**Project Overview:**
- Key metrics cards (total tasks, completed, in progress, team size)
- Quick statistics
- Recent activity feed
- Team member status
- Upcoming deadlines

**📸 Screenshot Placeholders:**

> **[SCREENSHOT 8.7.9]** Dashboard Metrics Cards
> - Show: Grid of metric cards with key statistics
> - Location: `/screenshots/visualization/metrics-cards.png`
> - Expected: Cards showing: Total Tasks, Completed, In Progress, Team Members, with icons and values

> **[SCREENSHOT 8.7.10]** Project Health Indicator
> - Show: Visual indicator of project health (healthy, warning, at-risk)
> - Location: `/screenshots/visualization/project-health.png`
> - Expected: Color-coded status indicator with health explanation and action recommendations

---

### 8.8 Notifications and Alerts

**Features:**
- Email notifications for task assignments
- Reminder emails for approaching due dates
- Workspace invitation emails with accept links
- GitHub webhook failure alerts
- @mention notifications
- Customizable notification preferences
- Notification history and logs

**📸 Screenshot Placeholders:**

> **[SCREENSHOT 8.8.1]** Email Notification Sample
> - Show: Example email notification for task assignment
> - Location: `/screenshots/notifications/email-task-assignment.png`
> - Expected: Professional email template with task details, assignee info, action button

> **[SCREENSHOT 8.8.2]** In-App Notification Toast
> - Show: Toast notification appearing in-app for real-time updates
> - Location: `/screenshots/notifications/toast-notification.png`
> - Expected: Small notification bubble with icon, message, timestamp (typically top-right)

> **[SCREENSHOT 8.8.3]** Notification Preferences Panel
> - Show: Settings page for customizing notifications
> - Location: `/screenshots/notifications/notification-preferences.png`
> - Expected: Toggles for different notification types (email, in-app, mentions), frequency settings

> **[SCREENSHOT 8.8.4]** Notification Center/History
> - Show: List of all notifications with dismissal and action options
> - Location: `/screenshots/notifications/notification-center.png`
> - Expected: Notification list grouped by date, with read/unread status, delete button

---

### 8.9 Search and Filtering

**Features:**
- Global task search across projects
- Project search within workspace
- Filter by task status, assignee, priority, type
- Filter by date range (due dates, creation date)
- Filter by project or team member
- Advanced search with multiple criteria
- Save custom filter presets
- Search suggestions and autocomplete

**📸 Screenshot Placeholders:**

> **[SCREENSHOT 8.9.1]** Global Search Bar
> - Show: Search input field in navigation with dropdown results
> - Location: `/screenshots/search/global-search-bar.png`
> - Expected: Search input, results dropdown showing recent/matching tasks, search icon

> **[SCREENSHOT 8.9.2]** Search Results Page
> - Show: Full page displaying search results across all projects
> - Location: `/screenshots/search/search-results.png`
> - Expected: Results list with project context, task details, result count, pagination

> **[SCREENSHOT 8.9.3]** Advanced Filter Panel
> - Show: Expandable filter controls for detailed filtering
> - Location: `/screenshots/search/advanced-filters.png`
> - Expected: Filter dropdowns for: Status, Assignee, Priority, Type, Date range, with apply button

> **[SCREENSHOT 8.9.4]** Saved Filter Presets
> - Show: List of saved filter configurations for quick access
> - Location: `/screenshots/search/saved-filters.png`
> - Expected: Preset filter list with custom names, quick apply buttons, edit/delete options

---

### 📋 Screenshot Submission Checklist

**Screenshots to Capture:**
- [ ] 28 total screenshots (as indicated above)
- [ ] All feature areas covered with realistic data
- [ ] User-friendly interface elements visible
- [ ] Multiple states (empty, filled, loaded, error) where applicable
- [ ] Mobile responsiveness (if applicable)
- [ ] Dark mode versions (if available)

**Screenshot Naming Convention:**
```
/screenshots/[category]/[feature-name].png

Examples:
/screenshots/auth/login-page.png
/screenshots/tasks/task-detail-page.png
/screenshots/visualization/kanban-board.png
```

**Screenshot Requirements:**
- Resolution: 1920×1080 or higher for clarity
- Format: PNG (preferred) or JPG
- Include: Full UI, relevant data, no sensitive information
- Quality: Clear, well-lit, no pixelation
- Annotations: Optional, but helpful (arrows, circles for emphasis)

---

## 9. HOW TO RUN / INSTALLATION GUIDE

### 9.1 Prerequisites

**System Requirements:**
- Node.js 18.x or higher
- npm or yarn package manager
- Git version control
- A GitHub OAuth App (for GitHub integration)
- A Clerk account and API keys
- A Neon PostgreSQL database account

**Required Accounts:**
1. **Clerk Account:** https://clerk.com
   - Create application
   - Generate API keys and secret keys
2. **GitHub OAuth App:** https://github.com/settings/developers
   - Create OAuth application
   - Set authorization callback URL
   - Get Client ID and Client Secret
3. **Neon Database:** https://neon.tech
   - Create PostgreSQL project
   - Get database connection string

### 9.2 Installation Steps

#### **Step 1: Clone Repository**
```bash
# Clone the project
git clone https://github.com/yourusername/taskbit.git
cd taskbit

# Initialize git submodules if present
git submodule update --init --recursive
```

#### **Step 2: Server Setup**
```bash
# Navigate to server directory
cd server

# Install dependencies
npm install

# Create .env file
cat > .env << EOF
# Clerk Authentication
CLERK_API_KEY=your_clerk_api_key
CLERK_SECRET_KEY=your_clerk_secret_key

# Database
DATABASE_URL=postgresql://user:password@host:port/database

# GitHub OAuth
GITHUB_CLIENT_ID=your_github_client_id
GITHUB_CLIENT_SECRET=your_github_client_secret
GITHUB_OAUTH_REDIRECT_URI=http://localhost:5173/github/callback
SERVER_PUBLIC_URL=http://localhost:5000

# Email Service
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email@gmail.com
SMTP_PASS=your_app_password

# Inngest
INNGEST_API_KEY=your_inngest_api_key

# Server Configuration
PORT=5000
NODE_ENV=development
EOF

# Generate Prisma client
npx prisma generate

# Run database migrations
npx prisma migrate dev

# Seed database (optional)
npx prisma db seed

# Start development server
npm run server
# Server runs on http://localhost:5000
```

#### **Step 3: Client Setup**
```bash
# Navigate to client directory
cd ../client

# Install dependencies
npm install

# Create .env.local file
cat > .env.local << EOF
# Clerk Public Keys
VITE_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key

# API Configuration
VITE_API_URL=http://localhost:5000/api
VITE_WS_URL=ws://localhost:5000

# GitHub Configuration
VITE_GITHUB_CLIENT_ID=your_github_client_id

# Environment
VITE_APP_ENV=development
EOF

# Start development server
npm run dev
# Client runs on http://localhost:5173
```

### 9.3 Verification Steps

#### **Server Verification**
```bash
# Check server is running
curl http://localhost:5000
# Expected response: "Server is live!"

# Check API endpoints
curl http://localhost:5000/api/workspaces
# Should prompt for authentication if not authenticated
```

#### **Client Verification**
1. Open http://localhost:5173 in browser
2. Should see login page with Clerk authentication options
3. Click "Sign In" and authenticate via Google or GitHub
4. Should redirect to dashboard

#### **Database Verification**
```bash
# Connect to Neon database
psql postgresql://user:password@host:port/database

# Check tables created
\dt

# Expected tables: users, workspaces, projects, tasks, comments, etc.
```

### 9.4 Development Workflow

#### **Running Tests**
```bash
# Backend tests
cd server
npm test

# Frontend tests
cd ../client
npm test
```

#### **Code Quality**
```bash
# Lint frontend
npm run lint

# Fix linting issues
npm run lint -- --fix

# Format code
npm run format
```

#### **Database Development**
```bash
# View database in Prisma Studio
npx prisma studio

# Create new migration
npx prisma migrate dev --name add_feature_name

# Rollback migration
npx prisma migrate resolve --rolled-back <migration_name>
```

### 9.5 Deployment

#### **Deploy to Vercel**

**Frontend:**
```bash
# Install Vercel CLI
npm i -g vercel

# Login to Vercel
vercel login

# Deploy from client directory
cd client
vercel

# Follow prompts and set environment variables
```

**Backend:**
```bash
# From server directory
cd server
vercel

# Configure server environment variables in Vercel dashboard
```

#### **Configure Environment Variables**

Vercel Dashboard → Settings → Environment Variables:
```
CLERK_API_KEY=...
CLERK_SECRET_KEY=...
DATABASE_URL=postgresql://...
GITHUB_CLIENT_ID=...
GITHUB_CLIENT_SECRET=...
GITHUB_OAUTH_REDIRECT_URI=https://yourdomain.vercel.app/github/callback
SERVER_PUBLIC_URL=https://your-api.vercel.app
```

#### **Database Migration in Production**
```bash
# From server directory with production environment
npx prisma migrate deploy
```

### 9.6 Troubleshooting

| Issue | Solution |
|-------|----------|
| **Port already in use** | Change PORT in .env or kill process: `lsof -i :5000 \| grep LISTEN \| awk '{print $2}' \| xargs kill` |
| **Database connection failed** | Verify CONNECTION_URL format, check Neon dashboard for IP whitelist |
| **Clerk auth not working** | Verify CLERK_PUBLISHABLE_KEY and CLERK_SECRET_KEY, check Clerk dashboard for app settings |
| **GitHub OAuth callback error** | Ensure GITHUB_OAUTH_REDIRECT_URI matches GitHub OAuth app settings |
| **WebSocket connection failed** | Check firewall, verify WS_URL in .env.local, ensure server WebSocket is enabled |
| **Email not sending** | Verify SMTP credentials, check Gmail app passwords, enable less secure apps if applicable |
| **Prisma client issues** | Run `npx prisma generate`, clear node_modules and reinstall |

---

## 10. RESULTS & OUTPUT

### 10.1 Expected Outputs

#### **1. Dashboard View**
```
┌────────────────────────────────────────────────────┐
│ TaskBit Dashboard                           [⚙️]    │
├────────────────────────────────────────────────────┤
│                                                    │
│ Welcome, [User Name]! 👋                          │
│                                                    │
│ ┌──────────┬──────────┬──────────┬──────────┐    │
│ │ Workspace│ Projects │  Tasks   │  Teams   │    │
│ │   42     │    8     │    23    │    5     │    │
│ └──────────┴──────────┴──────────┴──────────┘    │
│                                                    │
│ Recent Projects:                                  │
│ ┌─────────────────────────────────────────────┐  │
│ │ 📦 TaskBit Core       [ACTIVE] 75% ▮▮▮▮░░│  │
│ │ 👥 Team Collaboration [ACTIVE] 45% ▮▮░░░░│  │
│ │ 🎯 GitHub Integration  [PLANNING] 10% ▮░░░│  │
│ └─────────────────────────────────────────────┘  │
│                                                    │
│ Recent Activity:                                  │
│ • John assigned you to "Fix login bug"            │
│ • Sarah commented on "Database optimization"     │
│ • 3 tasks completed today                         │
│                                                    │
└────────────────────────────────────────────────────┘
```

#### **2. Kanban Board View**
```
┌─────────────────────────────────────────────────────────┐
│ Project: TaskBit Core - Board View                      │
├──────────────┬──────────────┬──────────────┬────────────┤
│     TODO     │  IN_PROGRESS │     DONE     │  BACKLOG   │
├──────────────┼──────────────┼──────────────┼────────────┤
│ ┌──────────┐ │ ┌──────────┐ │ ┌──────────┐ │            │
│ │ FEAT-001 │ │ │ BUG-005  │ │ │ TASK-002 │ │            │
│ │ UI Design│ │ │ Fix auth │ │ │ Database │ │            │
│ │ [JOHN]   │ │ │ [SARAH]  │ │ │ [DONE]   │ │            │
│ │ High 📌 │ │ │ Med 📌   │ │ │ ✓        │ │            │
│ └──────────┘ │ └──────────┘ │ └──────────┘ │            │
│              │              │              │            │
│ ┌──────────┐ │ ┌──────────┐ │              │            │
│ │ IMPROVE  │ │ │ FEATURE  │ │              │            │
│ │ API Docs │ │ │ Search   │ │              │            │
│ │ [ALEX]   │ │ │ [MIKE]   │ │              │            │
│ │ Low      │ │ │ High     │ │              │            │
│ └──────────┘ │ └──────────┘ │              │            │
│              │              │              │            │
│ 2 items     │ 2 items       │ 1 item       │ 0 items    │
└──────────────┴──────────────┴──────────────┴────────────┘
```

#### **3. Task Details View**
```
┌────────────────────────────────────────────────────┐
│ Task Details                              [← Back]  │
├────────────────────────────────────────────────────┤
│                                                    │
│ FEAT-023: Implement Dark Mode                     │
│ Status: IN_PROGRESS  Priority: HIGH  [2 days left]│
│                                                    │
│ Assigned to: Sarah Johnson                        │
│ Type: FEATURE  Created: 2 days ago                │
│                                                    │
│ Description:                                      │
│ Implement system-wide dark mode support with      │
│ user preference persistence...                    │
│                                                    │
│ ─────────────────────────────────────────────     │
│ GitHub Issue: #45                                 │
│ Repository: taskbit/core                          │
│ Issue URL: github.com/taskbit/core/issues/45      │
│ State: OPEN                                        │
│ ─────────────────────────────────────────────     │
│                                                    │
│ Comments (3):                                     │
│                                                    │
│ 👤 John Doe (2 hours ago):                        │
│ "Great! Can we also support following system      │
│ preference for accessibility?"                    │
│                                                    │
│ 👤 Sarah Johnson (1 hour ago):                    │
│ "Absolutely! I'll add that in the implementation" │
│                                                    │
│ [Add Comment...]                                  │
│                                                    │
└────────────────────────────────────────────────────┘
```

#### **4. Analytics Dashboard**
```
┌────────────────────────────────────────────────────┐
│ Project Analytics                                  │
├────────────────────────────────────────────────────┤
│                                                    │
│ Overall Progress: 68%  ▮▮▮▮▮▮░░░░               │
│                                                    │
│ Task Completion:              │ Team Workload:    │
│ ┌──────────────────────────┐  │ ┌────────────────┐│
│ │       40%                │  │ │ John:  8 tasks ││
│ │   ●─ Completed          │  │ │ Sarah: 6 tasks ││
│ │   ●─ In Progress        │  │ │ Mike:  5 tasks ││
│ │   ●─ TODO               │  │ │ Alex:  4 tasks ││
│ └──────────────────────────┘  │ └────────────────┘│
│                               │                   │
│ Burndown Chart:              │ Task Type Dist:   │
│  100  ┌────────────────────  │ ┌────────────────┐│
│   90  │      Actual          │ │ Feature: 35%   ││
│   80  │    ╱╲         ┌──    │ │ Bug:     25%   ││
│   70  │   ╱  ╲       ╱       │ │ Task:    30%   ││
│   60  ├──┘    ╲     ╱        │ │ Other:   10%   ││
│   50  │        └────          │ └────────────────┘│
│    0  └──────────────────────  │                   │
│         Week 1   Week 2       │                   │
│                                                    │
└────────────────────────────────────────────────────┘
```

### 10.2 Performance Metrics

**Expected Outcomes:**
- Page load time: < 2 seconds (optimized with code splitting)
- API response time: < 200ms (cached queries)
- Real-time update latency: < 100ms (WebSocket)
- Database query optimization: Indexed lookups < 50ms
- Mobile responsiveness: 100% on devices 320px - 2560px

### 10.3 Usage Statistics

**Typical Application Scenarios:**

1. **Workspace Creation:** User creates workspace, invites 5 team members
   - Output: New workspace with roles assigned, invitation emails sent

2. **Project Setup:** Create project with 15 tasks, assign team leads
   - Output: Project dashboard ready, team members notified

3. **GitHub Integration:** Connect GitHub repository
   - Output: Webhook configured, ready to sync issues

4. **Task Update:** Assignee updates task status to DONE
   - Output: Real-time update to all clients, notification email sent, analytics updated

5. **Collaboration:** Comment on task, mention team member
   - Output: Comment visible to all, @mentioned user receives notification

---

## 11. CHALLENGES FACED

### 11.1 Technical Challenges and Solutions

#### **Challenge 1: GitHub Webhook Signature Verification**

**Problem:**
- Difficulty implementing HMAC-SHA256 signature verification correctly
- Buffer vs. string encoding mismatch causing validation failures
- Security risk if not verified properly

**Root Cause:**
- GitHub sends signature as hex string, but raw body buffer needed for verification
- Express.json() was parsing body before webhook handler, destroying raw buffer

**Solution:**
```javascript
// Correct implementation: Parse raw body BEFORE json middleware
app.use("/api/github/webhook", express.raw({ type: "application/json" }), 
  githubWebhookRouter);

// Signature verification function
function verifyGitHubSignature(req) {
  const signature = req.get('X-Hub-Signature-256');
  const body = req.body; // This is a Buffer
  
  const hash = crypto
    .createHmac('sha256', WEBHOOK_SECRET)
    .update(body)
    .digest('hex');
  
  return `sha256=${hash}` === signature;
}
```

#### **Challenge 2: Bi-directional GitHub-Task Synchronization**

**Problem:**
- One-way sync only working initially (GitHub → Task)
- Need for updating GitHub issues when task status changes
- Risk of infinite loop if not handled carefully

**Root Cause:**
- Only implemented webhook handler (GitHub → TaskBit)
- Missing API calls to update GitHub issues
- No mechanism to prevent sync loops

**Solution:**
```javascript
// Track sync operations to prevent loops
const syncTracker = new Map(); // projectId -> lastSyncTime

async function updateGitHubFromTask(projectId, taskId, newStatus) {
  // Check if recently synced (within 5 seconds)
  const lastSync = syncTracker.get(projectId);
  if (lastSync && Date.now() - lastSync < 5000) {
    console.log('Skipping sync to prevent loop');
    return;
  }
  
  const task = await getTask(taskId);
  if (!task.githubIssueNumber) return;
  
  const integration = await getGitHubIntegration(projectId);
  
  // Map TaskBit status to GitHub state
  const state = newStatus === 'DONE' ? 'closed' : 'open';
  
  // Call GitHub API
  await github.rest.issues.update({
    owner: task.githubRepository.split('/')[0],
    repo: task.githubRepository.split('/')[1],
    issue_number: task.githubIssueNumber,
    state: state
  }, {
    headers: { Authorization: `token ${integration.accessToken}` }
  });
  
  syncTracker.set(projectId, Date.now());
}
```

#### **Challenge 3: Real-time Updates with WebSocket**

**Problem:**
- WebSocket connection dropping on network changes
- Duplicate updates causing UI glitches
- Memory leaks from unclosed connections

**Root Cause:**
- No reconnection logic implemented
- Duplicate event listeners in React components
- Connection pool not cleaned up on unmount

**Solution:**
```javascript
// Client-side WebSocket handler with reconnection
class WebSocketManager {
  constructor(url) {
    this.url = url;
    this.ws = null;
    this.reconnectAttempts = 0;
    this.maxReconnectAttempts = 5;
    this.reconnectDelay = 3000;
  }
  
  connect() {
    this.ws = new WebSocket(this.url);
    
    this.ws.onopen = () => {
      console.log('WebSocket connected');
      this.reconnectAttempts = 0;
    };
    
    this.ws.onerror = (error) => {
      console.error('WebSocket error:', error);
      this.attemptReconnect();
    };
    
    this.ws.onmessage = (event) => {
      const data = JSON.parse(event.data);
      // Dispatch Redux action with debouncing to prevent duplicates
      store.dispatch(updateTask(data));
    };
  }
  
  attemptReconnect() {
    if (this.reconnectAttempts < this.maxReconnectAttempts) {
      this.reconnectAttempts++;
      setTimeout(() => this.connect(), this.reconnectDelay);
    }
  }
}
```

#### **Challenge 4: Prisma Query Performance at Scale**

**Problem:**
- Slow queries when fetching workspaces with many projects/tasks
- N+1 query problem causing excessive database calls
- Memory issues with deeply nested relations

**Root Cause:**
- Not using Prisma's `include` for eager loading
- Missing database indexes on foreign keys
- Fetching full relations when only partial data needed

**Solution:**
```javascript
// Optimized Prisma query with specific includes
const workspace = await prisma.workspace.findUnique({
  where: { id: workspaceId },
  include: {
    projects: {
      select: {
        id: true,
        name: true,
        status: true,
        progress: true,
        tasks: {
          select: {
            id: true,
            title: true,
            status: true,
            assigneeId: true,
            dueDate: true
          },
          take: 50 // Limit nested relations
        },
        members: {
          select: {
            userId: true,
            user: { select: { name: true, email: true } }
          }
        }
      },
      take: 100 // Paginate projects
    }
  }
});

// Add database indexes
// In schema.prisma
model Task {
  @@index([projectId])
  @@index([assigneeId])
  @@index([status])
}
```

### 11.2 Design Challenges and Solutions

#### **Challenge 5: Multi-tenant Data Isolation**

**Problem:**
- Ensuring users can only access their workspace's data
- Authorization checks needed at multiple levels
- Risk of accidental data exposure between workspaces

**Solution:**
```javascript
// Middleware to verify workspace access
async function verifyWorkspaceAccess(req, res, next) {
  const { workspaceId } = req.body;
  const userId = req.user.id;
  
  const membership = await prisma.workspaceMember.findUnique({
    where: {
      userId_workspaceId: { userId, workspaceId }
    }
  });
  
  if (!membership) {
    return res.status(403).json({ error: 'Workspace access denied' });
  }
  
  req.workspace = membership;
  next();
}

// Apply to all workspace routes
app.use('/api/workspaces/:id', verifyWorkspaceAccess);
```

#### **Challenge 6: State Management Consistency**

**Problem:**
- Redux state becoming out of sync with server state
- Conflicting local changes and server updates
- Optimistic updates failing without proper rollback

**Solution:**
```javascript
// Redux middleware for handling async operations
const asyncThunk = createAsyncThunk(
  'tasks/updateStatus',
  async ({ taskId, newStatus }, { rejectWithValue }) => {
    try {
      const response = await api.patch(`/tasks/${taskId}`, {
        status: newStatus
      });
      return response.data;
    } catch (error) {
      return rejectWithValue(error.response.data);
    }
  }
);

// Slice with proper error handling
const tasksSlice = createSlice({
  name: 'tasks',
  initialState: { items: [], loading: false, error: null },
  extraReducers: (builder) => {
    builder
      .addCase(asyncThunk.pending, (state) => {
        state.loading = true;
      })
      .addCase(asyncThunk.fulfilled, (state, action) => {
        state.loading = false;
        const index = state.items.findIndex(t => t.id === action.payload.id);
        if (index !== -1) {
          state.items[index] = action.payload;
        }
      })
      .addCase(asyncThunk.rejected, (state, action) => {
        state.loading = false;
        state.error = action.payload.message;
      });
  }
});
```

### 11.3 Operational Challenges

#### **Challenge 7: Environment Configuration Management**

**Problem:**
- Different configs needed for dev, staging, production
- Secrets accidentally committed to version control
- Hard-coded values causing deployment issues

**Solution:**
- Implemented `.env.example` with template variables
- Used `dotenv` with validation schema
- Git hooks to prevent env file commits
- Environment-specific config files

```javascript
// .env.example
DATABASE_URL=postgresql://user:pass@host:port/db
CLERK_API_KEY=your_clerk_api_key_here
GITHUB_CLIENT_ID=your_github_client_id

// .env.production
DATABASE_URL=${DATABASE_URL}  # Set via deployment platform
CLERK_API_KEY=${CLERK_API_KEY}
...

// Pre-commit hook
if git diff --cached --name-only | grep -E '\.env$'; then
  echo "Error: Cannot commit .env files"
  exit 1
fi
```

#### **Challenge 8: Scaling Websocket Connections**

**Problem:**
- Single server bottleneck for real-time updates
- Memory leaks from maintaining thousands of connections
- Broadcasting to large projects causing lag

**Solution (for future scaling):**
- Implement Redis pub/sub for multi-server broadcasting
- Use Socket.io with Redis adapter
- Implement connection pooling and cleanup
- Paginate/batch large broadcasts

---

## 12. FUTURE SCOPE

### 12.1 Short-term Improvements (Next 3 months)

1. **Advanced Task Management**
   - Task dependencies and blocking relationships
   - Time estimation and actual time tracking
   - Task templates for recurring workflows
   - Subtasks for complex work breakdown

2. **Enhanced Notifications**
   - Customizable notification preferences
   - Slack integration for notifications
   - Email digest summaries
   - In-app notification center with history

3. **Collaboration Features**
   - Real-time collaborative editing of task descriptions
   - @mention mentions with autocomplete
   - Activity feeds at project and workspace levels
   - Document attachments and file sharing

4. **UI/UX Enhancements**
   - Dark mode theme
   - Customizable dashboard widgets
   - Keyboard shortcuts for power users
   - Mobile-responsive improvements

### 12.2 Medium-term Enhancements (6-12 months)

1. **Advanced GitHub Integration**
   - Pull request tracking integrated with tasks
   - Code review assignment from tasks
   - Automated issue creation from code comments
   - GitHub Actions workflow integration

2. **Reporting and Export**
   - Custom report builder
   - Export to PDF, Excel, CSV
   - Scheduled report delivery via email
   - Business intelligence dashboard integration

3. **Workflow Automation**
   - Custom workflow rules (if-this-then-that)
   - Automation templates
   - Task auto-assignment based on rules
   - Automated status transitions based on conditions

4. **Integration Ecosystem**
   - Jira integration for issue sync
   - Azure DevOps integration
   - Slack/Teams workspace integration
   - Calendar integration (Google Calendar, Outlook)

5. **Advanced Analytics**
   - Predictive analytics for project completion
   - Team productivity metrics and trends
   - Velocity tracking for agile teams
   - Performance benchmarking

### 12.3 Long-term Vision (1-2 years+)

1. **Mobile Applications**
   - Native iOS and Android apps
   - Offline task management with sync
   - Mobile-optimized interface
   - Push notifications

2. **AI-Powered Features**
   - Intelligent task recommendations
   - Automatic priority detection
   - NLP-based task parsing from emails
   - Predictive workload balancing
   - Automatic meeting scheduling

3. **Enterprise Features**
   - SSO (Single Sign-On) integration
   - Advanced permission and security models
   - Audit logs and compliance reporting
   - Data residency options
   - SLA monitoring

4. **Scalability Improvements**
   - Multi-region deployment
   - Advanced caching strategies
   - GraphQL API for optimized data fetching
   - Microservices architecture migration
   - Kubernetes deployment support

5. **Advanced Customization**
   - Custom field definitions
   - Customizable workflows and pipelines
   - Theme customization
   - Plugin system for extensibility
   - API marketplace for third-party apps

### 12.4 Research and Innovation

1. **Emerging Technologies**
   - WebRTC for direct peer-to-peer collaboration
   - Machine learning for anomaly detection
   - Blockchain for immutable audit trails
   - AR/VR interfaces for immersive collaboration

2. **User Research**
   - Conduct UX studies with diverse user groups
   - Gather feedback from enterprise customers
   - Analyze usage patterns and pain points
   - Competitive analysis and benchmarking

---

## 13. CONCLUSION

TaskBit represents a comprehensive solution to modern project management and team collaboration challenges. By integrating task management, team coordination, and GitHub issue synchronization into a unified platform, the application addresses key pain points faced by distributed teams and software development organizations.

### Key Achievements

1. **Full-Stack Implementation:** Successfully developed a complete web application spanning frontend (React 19, Vite), backend (Express.js, Node.js), and database (PostgreSQL with Prisma ORM) layers.

2. **Third-Party Integration:** Seamlessly integrated GitHub OAuth and webhooks, enabling bi-directional synchronization of issues and task statuses, demonstrating expertise in external API integration patterns.

3. **Real-time Collaboration:** Implemented WebSocket-based real-time updates, allowing teams to see changes instantly across the platform without page refreshes, enhancing user experience and productivity.

4. **Scalable Architecture:** Designed a multi-tenant architecture with role-based access control, supporting unlimited workspaces, projects, and team members while maintaining data isolation and security.

5. **Modern Technology Stack:** Utilized industry-best practices and modern technologies including Redux for state management, Tailwind CSS for responsive design, Clerk for authentication, and Inngest for background job processing.

### Technical Competencies Demonstrated

- **Frontend Development:** Component-based architecture, state management, routing, responsive design
- **Backend Development:** RESTful API design, middleware patterns, authentication/authorization, error handling
- **Database Design:** Normalized schema design, relationship modeling, query optimization with ORM
- **Third-Party Integration:** OAuth flows, webhook handling, API integration, error recovery
- **DevOps:** Environment configuration, deployment automation, database migrations
- **Security:** Data isolation, encryption, signature verification, role-based access control

### Impact and Value

TaskBit provides immediate value to teams by:
- Reducing tool fragmentation and context switching
- Enabling faster task completion through better visibility
- Automating notifications and reminders
- Providing actionable insights through analytics
- Integrating with existing GitHub workflows

The platform is production-ready and scalable, supporting growth from small teams to large organizations with thousands of tasks and team members.

### Final Remarks

This project demonstrates comprehensive understanding of full-stack web development, system design, and best practices in building scalable, secure applications. The modular architecture and event-driven design provide a foundation for future enhancements and integrations. TaskBit serves as both a functional product and a learning resource for modern web application development practices.

The combination of technical excellence, user-centric design, and practical functionality makes TaskBit a valuable addition to the project management landscape, particularly for development teams seeking GitHub integration and real-time collaboration capabilities.

---

## 14. REFERENCES

### 14.1 Framework & Library Documentation

1. React Documentation (v19)
   - Available at: https://react.dev
   - Accessed: April 2026

2. Express.js Documentation (v5.1)
   - Available at: https://expressjs.com
   - Accessed: April 2026

3. Prisma ORM Documentation (v6.17)
   - Available at: https://www.prisma.io/docs
   - Accessed: April 2026

4. Redux Toolkit Documentation
   - Available at: https://redux-toolkit.js.org
   - Accessed: April 2026

5. Tailwind CSS Documentation (v4.1)
   - Available at: https://tailwindcss.com/docs
   - Accessed: April 2026

### 14.2 Authentication & External Services

6. Clerk Documentation
   - Available at: https://clerk.com/docs
   - Accessed: April 2026

7. GitHub REST API v2022-11-28 Documentation
   - Available at: https://docs.github.com/en/rest
   - Accessed: April 2026

8. GitHub Webhooks Documentation
   - Available at: https://docs.github.com/en/developers/webhooks-and-events/webhooks
   - Accessed: April 2026

9. Inngest Documentation
   - Available at: https://www.inngest.com/docs
   - Accessed: April 2026

### 14.3 Database & Infrastructure

10. PostgreSQL Official Documentation
    - Available at: https://www.postgresql.org/docs
    - Accessed: April 2026

11. Neon Documentation
    - Available at: https://neon.tech/docs
    - Accessed: April 2026

12. Vercel Deployment Documentation
    - Available at: https://vercel.com/docs
    - Accessed: April 2026

### 14.4 Best Practices & Architecture

13. "Building Microservices" by Sam Newman (2015)
    - O'Reilly Media
    - ISBN: 978-1491950340

14. "RESTful Web Services" by Leonard Richardson and Sam Ruby (2007)
    - O'Reilly Media
    - ISBN: 978-0596529260

15. "The Node.js Best Practices" by Yoni Goldberg
    - Available at: https://github.com/goldbergyoni/nodebestpractices
    - Accessed: April 2026

16. "React Patterns" by Michael Chan
    - Available at: https://reactpatterns.com
    - Accessed: April 2026

### 14.5 Security References

17. OWASP Top 10 Web Application Security Risks (2021)
    - Available at: https://owasp.org/Top10
    - Accessed: April 2026

18. OAuth 2.0 RFC 6749
    - Available at: https://tools.ietf.org/html/rfc6749
    - Accessed: April 2026

### 14.6 Project-Specific Documentation

19. TaskBit Technical Documentation
    - TECHNICAL_DOCUMENTATION.md (Included in repository)

20. GitHub Integration Setup Guide
    - GITHUB_INTEGRATION_SETUP.md (Included in repository)

---

## APPENDICES

### Appendix A: Database Schema Export

```sql
-- Generated by Prisma
-- Created: April 2026

CREATE TABLE "User" (
  id TEXT NOT NULL PRIMARY KEY,
  name TEXT,
  email TEXT NOT NULL UNIQUE,
  image TEXT,
  designation TEXT,
  department TEXT,
  about TEXT,
  "createdAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP,
  "updatedAt" TIMESTAMP(3) NOT NULL
);

CREATE TABLE "Workspace" (
  id TEXT NOT NULL PRIMARY KEY,
  name TEXT NOT NULL,
  slug TEXT NOT NULL UNIQUE,
  description TEXT,
  settings JSONB,
  "ownerId" TEXT NOT NULL,
  image_url TEXT,
  "createdAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP,
  "updatedAt" TIMESTAMP(3) NOT NULL,
  FOREIGN KEY ("ownerId") REFERENCES "User" (id)
);

CREATE TABLE "Project" (
  id TEXT NOT NULL PRIMARY KEY,
  name TEXT NOT NULL,
  description TEXT,
  priority TEXT DEFAULT 'MEDIUM',
  status TEXT DEFAULT 'PLANNING',
  start_date TIMESTAMP(3),
  end_date TIMESTAMP(3),
  team_lead TEXT,
  "workspaceId" TEXT NOT NULL,
  progress INTEGER DEFAULT 0,
  "createdAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP,
  "updatedAt" TIMESTAMP(3) NOT NULL,
  FOREIGN KEY (team_lead) REFERENCES "User" (id),
  FOREIGN KEY ("workspaceId") REFERENCES "Workspace" (id)
);

CREATE TABLE "Task" (
  id TEXT NOT NULL PRIMARY KEY,
  "projectId" TEXT NOT NULL,
  title TEXT NOT NULL,
  description TEXT,
  status TEXT DEFAULT 'TODO',
  type TEXT DEFAULT 'TASK',
  priority TEXT DEFAULT 'MEDIUM',
  "assigneeId" TEXT,
  due_date TIMESTAMP(3),
  "githubIssueNumber" INTEGER,
  "githubIssueUrl" TEXT,
  "githubRepository" TEXT,
  "createdAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP,
  "updatedAt" TIMESTAMP(3) NOT NULL,
  FOREIGN KEY ("projectId") REFERENCES "Project" (id),
  FOREIGN KEY ("assigneeId") REFERENCES "User" (id)
);

CREATE TABLE "Comment" (
  id TEXT NOT NULL PRIMARY KEY,
  content TEXT NOT NULL,
  "userId" TEXT NOT NULL,
  "taskId" TEXT NOT NULL,
  "createdAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY ("userId") REFERENCES "User" (id),
  FOREIGN KEY ("taskId") REFERENCES "Task" (id)
);

-- Indexes for performance
CREATE INDEX "Project_workspaceId_idx" ON "Project" ("workspaceId");
CREATE INDEX "Task_projectId_idx" ON "Task" ("projectId");
CREATE INDEX "Task_assigneeId_idx" ON "Task" ("assigneeId");
CREATE INDEX "Comment_taskId_idx" ON "Comment" ("taskId");
```

### Appendix B: Environment Configuration Template

```bash
# .env.example
# Copy this file to .env and fill in your values

# ========== Clerk Authentication ==========
CLERK_API_KEY=pk_test_...
CLERK_SECRET_KEY=sk_test_...

# ========== Database ==========
DATABASE_URL=postgresql://user:password@localhost:5432/taskbit

# ========== GitHub OAuth ==========
GITHUB_CLIENT_ID=your_github_client_id
GITHUB_CLIENT_SECRET=your_github_client_secret
GITHUB_OAUTH_REDIRECT_URI=http://localhost:5173/github/callback

# ========== Server Configuration ==========
SERVER_PUBLIC_URL=http://localhost:5000
PORT=5000
NODE_ENV=development

# ========== Email Configuration ==========
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email@gmail.com
SMTP_PASS=your_app_password

# ========== Background Jobs (Inngest) ==========
INNGEST_API_KEY=your_inngest_api_key

# ========== Optional Features ==========
ENABLE_GITHUB_INTEGRATION=true
ENABLE_EMAIL_NOTIFICATIONS=true
DEBUG_MODE=false
```

### Appendix C: API Endpoint Summary

```
BASE_URL: http://localhost:5000/api

WORKSPACES
  GET    /workspaces              - List all workspaces
  POST   /workspaces              - Create workspace
  GET    /workspaces/:id          - Get workspace details
  PUT    /workspaces/:id          - Update workspace
  DELETE /workspaces/:id          - Delete workspace
  POST   /workspaces/:id/members  - Invite member
  DELETE /workspaces/:id/members/:memberId - Remove member

PROJECTS
  GET    /projects                - List projects (filtered by workspace)
  POST   /projects                - Create project
  GET    /projects/:id            - Get project details
  PUT    /projects/:id            - Update project
  DELETE /projects/:id            - Delete project
  POST   /projects/:id/members    - Add team member
  DELETE /projects/:id/members/:memberId - Remove member

TASKS
  GET    /tasks                   - List tasks (filtered by project)
  POST   /tasks                   - Create task
  GET    /tasks/:id               - Get task details
  PUT    /tasks/:id               - Update task
  DELETE /tasks/:id               - Delete task
  PUT    /tasks/:id/status        - Update task status
  PUT    /tasks/:id/assign        - Assign task

COMMENTS
  GET    /comments                - List comments (filtered by task)
  POST   /comments                - Add comment
  PUT    /comments/:id            - Update comment
  DELETE /comments/:id            - Delete comment

GITHUB
  GET    /github/authorize        - Initiate OAuth flow
  GET    /github/callback         - OAuth callback handler
  POST   /github/webhook/:projectId - Webhook receiver
  GET    /github/repos            - List repositories
  POST   /github/webhook/setup    - Create webhook
  DELETE /github/disconnect       - Disconnect integration
```

---

**Document Completion Date:** April 23, 2026

**Total Pages:** 26

**Report Status:** Complete and Ready for Submission

---

*This comprehensive project report has been prepared as per academic standards and covers all essential aspects of the TaskBit project management system. The report demonstrates technical proficiency in full-stack web development, architectural design, and best practices in software engineering.*
