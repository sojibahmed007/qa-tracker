# QA Tracker — Professional QA Workspace & Test Management Web Application

[![Live Demo](https://img.shields.io/badge/Live%20Demo-Vercel%20Production-success?style=for-the-badge&logo=vercel)](https://qa-tracker-workspace.vercel.app)
[![Tests](https://img.shields.io/badge/Tests-32%20Passed-emerald?style=for-the-badge&logo=vitest)](https://qa-tracker-workspace.vercel.app)
[![TypeScript](https://img.shields.io/badge/TypeScript-Strict-blue?style=for-the-badge&logo=typescript)](https://qa-tracker-workspace.vercel.app)
[![License: MIT](https://img.shields.io/badge/License-MIT-purple?style=for-the-badge)](LICENSE)

**QA Tracker** is a production-grade, responsive QA workspace designed for Software Quality Assurance (SQA) Engineers to organize projects, track feature workflows, manage test repositories, execute manual test suites across multiple environments, document bugs, and manage external Jira/Trello task cards.

🔗 **Live Application URL**: [https://qa-tracker-workspace.vercel.app](https://qa-tracker-workspace.vercel.app)

---

## 🌟 Key Capabilities

1. **Jira & Trello Personal Task Cards Hub**:
   - Dedicated Kanban & List board to organize external Jira, Trello, Linear, or GitHub tickets.
   - Attach ticket keys (e.g. `PROJ-102`), direct URLs, notes, priorities, deadlines, and QA progress (`To Do`, `In Progress`, `In QA`, `Blocked`, `Done`).
   - Live KPI counters synchronized across the main Dashboard metrics, project carousel pills, and hero banner.

2. **Multi-Environment Testing Pipeline**:
   - Distinct testing progression across **Development**, **Staging**, and **Production**.
   - Independent execution metrics and status per environment.
   - Milestone celebration banner upon 100% completion of any target environment.

3. **Multi-Project & Feature Hierarchy**:
   - Organize applications by project (Web, Mobile Android/iOS, API, Other).
   - Break projects down into features (e.g. *Login*, *Registration*, *Product Catalog*, *Checkout*, *Profile Settings*).
   - Dedicated 6-tab feature workspace: **Overview**, **Test Cases**, **Test Execution**, **Bug Reports**, **Notes**, and **Activity History**.

4. **Essential Test Case File Import (No AI Required)**:
   - Import test cases directly from **CSV**, **Excel (`.xlsx`)**, **JSON**, or direct **Copy-Paste** from Google Sheets or Excel tables.
   - Intelligent column auto-detection and custom column mapping with prominent display of ID, Title, Steps, and Expected Result.
   - Interactive preview with validation (required fields highlighted) and duplicate ID detection.
   - Inline row editing and row toggles before saving.

5. **Manual Test Case Authoring**:
   - Detailed specifications: Test ID (e.g. `TC_LOGIN_001`), Title, Objective, Preconditions, Test Data, Action Steps, Expected Result, Priority, and Test Type.
   - Collision-prevention for human-readable IDs.
   - Duplicate, edit, bulk delete, and status updates.

6. **Preserved Test Execution History**:
   - Record execution status (`Pass`, `Fail`, `Blocked`, `Not Run`), actual result, tester name, environment, and build version.
   - Full chronological execution history log per test case — previous runs are never silently overwritten.
   - Rerun tests and compare results across staging and production builds.

7. **Integrated Defect / Bug Management**:
   - File defects directly from failed test runs with pre-filled test case details, steps, and observed outcomes.
   - Lifecycle progression: `Open` ➔ `In Progress` ➔ `Fixed` ➔ `Ready for Retest` ➔ `Closed` / `Reopened`.
   - Filter by severity, priority, status, and project.

8. **Optional AI Test Case Generator**:
   - Modular, independent AI assistant powered by Google Gemini.
   - Generates structured test suites based on user stories, user roles, business rules, and test categories (*Positive*, *Negative*, *Boundary*, *Validation*, *Security*, *Permission*).
   - Reviews, labels assumptions clearly, and allows approval before committing to the database.

9. **Flexible Backend: Cloud Supabase or Built-In Offline Engine**:
   - Seamlessly connects to **Supabase PostgreSQL** with full **Row Level Security (RLS)** policies.
   - Built-in zero-friction **Offline / Demo Local Storage Engine** with pre-seeded sample data (*CloudCommerce Demo*) for immediate test drives.

10. **Export & Backup**:
    - Export test cases to **CSV** and **Excel (`.xlsx`)**.
    - Export defect reports to **CSV**.
    - Generate full workspace **JSON snapshots** and restore with schema validation.

---

## 🏗️ Architecture & Technology Stack

| Layer | Technologies |
| :--- | :--- |
| **Frontend Framework** | React 19 + TypeScript + Vite |
| **Styling** | Tailwind CSS (Dark/Light mode support) |
| **Routing** | React Router v7 |
| **Icons** | Lucide React |
| **File Parsing** | Papa Parse (CSV/TSV), SheetJS `xlsx` (Excel) |
| **Backend & Database** | Supabase PostgreSQL with Row Level Security (RLS) |
| **Authentication** | Supabase Auth (Email/Password, Session Persistence, Password Reset) |
| **Unit Testing** | Vitest + Testing Library + JSDOM |
| **E2E Testing** | Playwright |
| **Hosting & Deployment**| Vercel Production + Supabase PostgreSQL |

---

## 📁 Project Folder Structure

```text
qa-tracker/
├── e2e/
│   └── qa-tracker.spec.ts         # Playwright End-to-End tests
├── public/                        # Static assets & icons
├── src/
│   ├── __tests__/                 # Vitest automated unit & integration tests
│   │   ├── calculations.test.ts   # Progress %, pass rate %, latest run logic
│   │   ├── csv-parser.test.ts     # CSV, Excel, TSV, column mapping & validation
│   │   ├── export-utils.test.ts   # Backup verification & export logic
│   │   ├── setup.ts               # Testing environment setup
│   │   └── storage-adapter.test.ts# Database operations & cascade deletion tests
│   ├── components/
│   │   ├── ai/
│   │   │   └── AITestCaseGenerator.tsx
│   │   ├── bugs/
│   │   │   └── BugModal.tsx
│   │   ├── common/
│   │   │   ├── Badge.tsx          # Status, priority, and severity badges
│   │   │   ├── Breadcrumbs.tsx    # Contextual navigation breadcrumbs
│   │   │   ├── ConfirmationDialog.tsx # Safe destructive action dialogs
│   │   │   ├── EmptyState.tsx     # Helpful empty state illustrations
│   │   │   ├── LoadingSpinner.tsx # High-contrast loading indicator
│   │   │   ├── Modal.tsx          # Accessible modal dialog
│   │   │   ├── Navbar.tsx         # Top bar with environment badge & theme switch
│   │   │   └── Sidebar.tsx        # Responsive navigation sidebar
│   │   ├── dashboard/
│   │   │   ├── MetricCards.tsx    # KPI progress and pass rate calculations
│   │   │   ├── ProjectsSummaryTable.tsx
│   │   │   ├── RecentActivityFeed.tsx
│   │   │   └── RecentFailuresList.tsx
│   │   ├── execution/
│   │   │   ├── ExecuteModal.tsx   # Run test modal with quick defect logger
│   │   │   └── ExecutionHistoryModal.tsx # Chronological run history
│   │   ├── features/
│   │   │   ├── FeatureActivity.tsx
│   │   │   ├── FeatureModal.tsx
│   │   │   ├── FeatureNotes.tsx
│   │   │   └── FeatureWorkspace.tsx # 6-tab feature workstation
│   │   ├── import/
│   │   │   └── TestCaseImporter.tsx # 5-step file import & validation wizard
│   │   ├── projects/
│   │   │   └── ProjectModal.tsx
│   │   └── test-cases/
│   │       ├── TestCaseDetailModal.tsx
│   │       └── TestCaseModal.tsx
│   ├── context/
│   │   ├── AuthContext.tsx        # Supabase Auth + Local Demo fallback
│   │   ├── ThemeContext.tsx       # Dark & light theme switcher
│   │   └── ToastContext.tsx       # Floating notification alert system
│   ├── lib/
│   │   ├── calculations.ts        # Pure math for progress & pass rate
│   │   ├── csv-parser.ts          # File parser & auto-column mapping
│   │   ├── export-utils.ts        # CSV, Excel, and JSON backup exports
│   │   ├── gemini-api.ts          # Gemini AI generation client
│   │   ├── storage-adapter.ts     # Unified Supabase + Local storage engine
│   │   └── supabase.ts            # Official Supabase client initializer
│   ├── pages/
│   │   ├── AIGeneratorPage.tsx
│   │   ├── BugsPage.tsx
│   │   ├── DashboardPage.tsx
│   │   ├── ForgotPasswordPage.tsx
│   │   ├── ImportExportPage.tsx
│   │   ├── LoginPage.tsx
│   │   ├── ProjectDetailPage.tsx
│   │   ├── ProjectsPage.tsx
│   │   ├── SettingsPage.tsx
│   │   ├── SignUpPage.tsx
│   │   └── TestCasesPage.tsx
│   ├── types/
│   │   └── database.ts            # Type definitions for all QA entities
│   ├── App.tsx                    # Route definitions & layout guard
│   ├── index.css                  # Tailwind styles and custom scrollbars
│   └── main.tsx                   # App entrypoint
├── supabase/
│   └── schema.sql                 # Complete PostgreSQL schema & RLS policies
├── .env.example                   # Environment configuration template
├── playwright.config.ts           # Playwright E2E configuration
├── tailwind.config.js             # Tailwind configuration
└── vitest.config.ts               # Vitest unit test configuration
```

---

## ⚡ Quick Start & Local Setup

### 1. Prerequisites
- Node.js `v18.0.0` or higher (`v22` recommended)
- `npm` or `pnpm`

### 2. Installation
Navigate to the project folder and install dependencies:
```bash
cd qa-tracker
npm install
```

### 3. Start Development Server
```bash
npm run dev
```
Open [http://localhost:5173](http://localhost:5173) in your browser.

> [!NOTE]
> **No Credentials Needed to Test Drive!**
> QA Tracker detects if Supabase is unconfigured and immediately offers **Instant Demo Workspace**. Click **"Launch Pre-Loaded Demo Workspace"** on the login screen to start exploring the pre-loaded **EzyCourse Demo** project right away.

---

## 🗄️ Supabase PostgreSQL Setup & RLS

When you are ready to connect to a real cloud database:

1. Create a free project at [https://supabase.com](https://supabase.com).
2. Go to the **SQL Editor** in your Supabase dashboard.
3. Open `supabase/schema.sql` in this project, copy its contents, paste them into the SQL editor, and click **Run**.
   - This sets up tables for `profiles`, `projects`, `features`, `test_cases`, `test_executions`, `bug_reports`, `feature_notes`, and `activity_logs`.
   - It enables **Row Level Security (RLS)** so that each user can only read, insert, update, or delete their own data.
   - It creates optimal database indexes and an automated profile creation trigger.
4. Copy your project credentials from **Project Settings ➔ API**:
   - `Project URL`
   - `anon public key`
5. Create a `.env` file in the root directory:
   ```env
   VITE_SUPABASE_URL=https://your-project-id.supabase.co
   VITE_SUPABASE_ANON_KEY=your-anon-key-here
   VITE_GEMINI_API_KEY=your-optional-gemini-key
   ```
6. Restart `npm run dev`. QA Tracker will automatically detect the Supabase connection and display **"Supabase Cloud Active"** in the top navigation bar.

---

## 🤖 Optional AI Configuration

- A Google Gemini API key is **completely optional**.
- Core features (manual creation, CSV/Excel/JSON/Paste import, test executions, bug tracking, export) function 100% offline without AI.
- To enable AI generation:
  1. Get a free Gemini key from [Google AI Studio](https://aistudio.google.com/app/apikey).
  2. Paste it in `.env` as `VITE_GEMINI_API_KEY=` or enter it directly in **Settings ➔ AI Provider Configuration**.

---

## 🧪 Running Automated Tests

### 1. Run Unit & Integration Tests (Vitest)
```bash
npm test
```
Runs 19 automated unit tests verifying:
- Test case import parsing & TSV/Markdown detection
- Column auto-mapping
- Priority and test type normalizers
- Step ordering preservation
- Required field validation and duplicate detection
- Accurate progress % and pass rate % math
- Database cascade deletions & run history preservation

### 2. Run End-to-End Tests (Playwright)
```bash
npx playwright test
```
Runs end-to-end user journeys including login, project creation, feature configuration, file import, test execution, and defect logging.

---

## 🚀 Production Build & Deployment

### Build for Production
```bash
npm run build
```
Generates an optimized, minified production bundle in the `dist/` directory.

### Deploying to Cloudflare Pages (Free Tier)
1. Push your repository to GitHub or GitLab.
2. In the [Cloudflare Dashboard](https://dash.cloudflare.com/), go to **Workers & Pages ➔ Create application ➔ Pages ➔ Connect to Git**.
3. Select the `qa-tracker` repository.
4. Set Build Settings:
   - **Framework preset**: `Vite`
   - **Build command**: `npm run build`
   - **Build output directory**: `dist`
5. Add Environment Variables:
   - `VITE_SUPABASE_URL` = your Supabase URL
   - `VITE_SUPABASE_ANON_KEY` = your Supabase anon key
   - `VITE_GEMINI_API_KEY` = (optional)
6. Click **Save and Deploy**. Cloudflare Pages will build and deploy your application globally.

---

## 📊 Calculation Standard

All metrics across the dashboard and feature workspaces follow strict SQA standards:
- **Execution Progress**:
  $$\text{Progress} = \frac{\text{Executed Test Cases}}{\text{Total Test Cases}} \times 100$$
  *(Executed includes `Pass`, `Fail`, and `Blocked`. `Not Run` is not executed).*
- **Pass Rate**:
  $$\text{Pass Rate} = \frac{\text{Passed Test Cases}}{\text{Executed Test Cases}} \times 100$$
  *(If Executed is 0, Pass Rate is 0%).*
- Calculations are derived from the **latest execution record** of each active test case while preserving all previous historical runs in `test_executions`.

---

## 📄 License
MIT License. Built for Software QA Engineers.
