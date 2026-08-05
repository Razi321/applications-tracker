# 📋 Applications Tracker — Product Requirements Document (PRD)

> **Author:** Razi  
> **Date:** August 5, 2026  
> **Duration:** 1-week side project  
> **Audience:** Junior developer (learning project)  
> **Repository:** You will create your own on GitHub (see Step 0)

---

## 0. Step Zero — GitHub Repo & PR Workflow

> [!IMPORTANT]
> **Do this FIRST before writing any code.** This is how real engineering teams work.

### 0.1 Create Your GitHub Repository

1. Go to [github.com/new](https://github.com/new)
2. **Repository name:** `applications-tracker`
3. **Description:** "Job applications tracker built with React + TypeScript"
4. **Visibility:** Public
5. Check **"Add a README file"**
6. Click **"Create repository"**
7. Clone it locally:
   ```bash
   git clone https://github.com/YOUR-USERNAME/applications-tracker.git
   cd applications-tracker
   ```

### 0.2 How You Will Work — Branch + PR + Merge

**You will NEVER commit directly to `main`.** Instead, for every piece of work:

```
main (protected) ← PR ← feature-branch (your work)
```

Here's the workflow you'll repeat every day:

#### 1️⃣ Create a branch
```bash
# Make sure you're on main and up to date
git checkout main
git pull origin main

# Create a new branch for today's work
git checkout -b day-1/project-setup
```

#### 2️⃣ Do your work, commit often
```bash
# Stage and commit your changes
git add .
git commit -m "feat: initialize Vite + React + TypeScript project"

# Push the branch to GitHub
git push origin day-1/project-setup
```

#### 3️⃣ Open a Pull Request on GitHub
1. Go to your repo on GitHub
2. You'll see a banner: **"day-1/project-setup had recent pushes — Compare & pull request"**
3. Click it
4. **Title:** `Day 1: Project Setup — Vite + React + TS + Tailwind`
5. **Description:** Write what you did (2-3 bullet points)
6. Click **"Create pull request"**

#### 4️⃣ Merge the PR
1. On the PR page, click **"Merge pull request"**
2. Click **"Confirm merge"**
3. Click **"Delete branch"** (keeps things clean)
4. Back in your terminal:
   ```bash
   git checkout main
   git pull origin main
   ```

### 0.3 Branch Naming Convention

Use this format: `day-N/short-description`

| Day | Branch Name | PR Title |
|-----|------------|----------|
| Day 1 | `day-1/project-setup` | Day 1: Project Setup |
| Day 2 | `day-2/types-and-layout` | Day 2: Types & Layout Components |
| Day 3 | `day-3/storage-and-data` | Day 3: Storage & Data Layer |
| Day 4 | `day-4/form-and-modal` | Day 4: Form & Modal |
| Day 5 | `day-5/edit-delete-status` | Day 5: Edit, Delete & Status |
| Day 6 | `day-6/search-filter-polish` | Day 6: Search, Filter & Polish |
| Day 7 | `day-7/deploy-and-readme` | Day 7: Deploy & README |

> [!TIP]
> **Commit often, not just once at the end of the day.** Good commits are small and describe one thing:
> - ✅ `feat: add ApplicationCard component`
> - ✅ `fix: status badge color not showing`
> - ✅ `style: add hover animation to cards`
> - ❌ `did stuff` 
> - ❌ `update`

### 0.4 Commit Message Format

Use prefixes so your git history is readable:

| Prefix | When to use | Example |
|--------|------------|----------|
| `feat:` | New feature | `feat: add delete confirmation dialog` |
| `fix:` | Bug fix | `fix: form not clearing after submit` |
| `style:` | CSS/styling only | `style: improve card hover effect` |
| `refactor:` | Code restructure (no behavior change) | `refactor: extract StatusBadge component` |
| `docs:` | Documentation | `docs: update README with screenshots` |
| `chore:` | Config/setup | `chore: configure Tailwind CSS` |

---

## 1. Product Overview

### What is it?
A **single-page web application** that helps job seekers track their job applications in one place — replacing messy spreadsheets with a clean, modern UI.

### Why build it?
- People use Excel/Google Sheets to track applications — it works but it's ugly and hard to filter
- A dedicated UI makes it faster to add, update, and visualize application status
- It's a great learning project that covers **React, TypeScript, Tailwind CSS, and modern tooling**

### Who is it for?
Anyone actively applying for jobs who wants a simple, free, private tracker that runs in their browser.

---

## 2. Tech Stack

| Layer | Technology | Why |
|-------|-----------|-----|
| **Framework** | [React 18+](https://react.dev/) | Component-based UI, industry standard |
| **Build Tool** | [Vite](https://vite.dev/) | Lightning-fast dev server & builds |
| **Language** | [TypeScript](https://www.typescriptlang.org/) | Type safety, better DX, industry standard |
| **Styling** | [Tailwind CSS v4](https://tailwindcss.com/) | Utility-first CSS, fast prototyping |
| **Storage** | `localStorage` | Free, no backend needed, data stays in the browser |
| **Hosting** | GitHub Pages | Free static hosting, deploys from the repo |
| **Version Control** | Git + GitHub | Track progress, learn git workflow |

### Prerequisites (Install Before Starting)
- **Node.js** (v18 or later) → [nodejs.org](https://nodejs.org/)
- **npm** (comes with Node.js)
- **Git** → [git-scm.com](https://git-scm.com/)
- **VS Code** (recommended) → [code.visualstudio.com](https://code.visualstudio.com/)

### Recommended VS Code Extensions
- `ES7+ React/Redux/React-Native snippets` — shortcut snippets for React
- `Tailwind CSS IntelliSense` — autocomplete for Tailwind classes
- `TypeScript Importer` — auto-import suggestions
- `Prettier` — code formatting

---

## 3. Project Setup (Day 1)

### 3.1 Initialize the Project

```bash
# Navigate to the project folder
cd ~/Desktop/applications-tracker

# Create Vite + React + TypeScript project in current directory
npx -y create-vite@latest ./ --template react-ts

# Install dependencies
npm install

# Install Tailwind CSS v4
npm install tailwindcss @tailwindcss/vite

# Start dev server
npm run dev
```

### 3.2 Configure Tailwind CSS

Add the Tailwind plugin to **`vite.config.ts`**:
```typescript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [
    react(),
    tailwindcss(),
  ],
  base: '/applications-tracker/',  // Required for GitHub Pages
})
```

Replace the contents of **`src/index.css`** with:
```css
@import "tailwindcss";
```

### 3.3 Configure GitHub Pages Deployment

Install the deployment package:
```bash
npm install --save-dev gh-pages
```

Add these scripts to **`package.json`**:
```json
{
  "scripts": {
    "predeploy": "npm run build",
    "deploy": "gh-pages -d dist"
  }
}
```

To deploy: `npm run deploy`  
Site will be live at: `https://razi321.github.io/applications-tracker/`

---

## 4. Features

### 4.1 Core Features (Must Have)

| # | Feature | Description |
|---|---------|-------------|
| F1 | **Add Application** | A modal form to add a new job application with all fields |
| F2 | **View Applications** | A card list or table showing all tracked applications |
| F3 | **Edit Application** | Click on an application to update its details |
| F4 | **Delete Application** | Remove an application with a confirmation prompt |
| F5 | **Status Tracking** | Update application status through predefined stages |
| F6 | **Persistent Storage** | Data saved in `localStorage` — survives page refresh |
| F7 | **Search & Filter** | Filter by status, search by company name or position |

### 4.2 Nice-to-Have Features (If Time Permits)

| # | Feature | Description |
|---|---------|-------------|
| N1 | **Dashboard Stats** | Summary cards: total apps, interviews, offers, rejections |
| N2 | **Sort by Date** | Sort applications by date applied (newest/oldest first) |
| N3 | **Export to CSV** | Download all data as a `.csv` file |
| N4 | **Import from CSV** | Upload a `.csv` to bulk-add applications |
| N5 | **Dark Mode Toggle** | Switch between light and dark themes |
| N6 | **Color-coded Status** | Each status gets a distinct color badge |

---

## 5. Data Model (TypeScript)

### 5.1 Types — create `src/types/index.ts`

```typescript
// All possible application statuses
export enum ApplicationStatus {
  Saved = "saved",
  Applied = "applied",
  InReview = "in_review",
  PhoneScreen = "phone_screen",
  Interview = "interview",
  Technical = "technical",
  FinalRound = "final_round",
  Offer = "offer",
  Accepted = "accepted",
  Rejected = "rejected",
  Withdrawn = "withdrawn",
}

// The main data shape for a job application
export interface Application {
  id: string;                    // Unique ID (use crypto.randomUUID())
  companyName: string;           // Required — Company name
  position: string;              // Required — Job title / role
  applicationUrl: string;        // Optional — Link to the job posting
  country: string;               // Optional — Country of the job
  location: string;              // Optional — City or "Remote"
  status: ApplicationStatus;     // Required — Current status
  dateApplied: string;           // Required — When applied (YYYY-MM-DD)
  dateUpdated: string;           // Auto-set — Last modification date
  salary: string;                // Optional — Salary range
  contactPerson: string;         // Optional — Recruiter / contact name
  notes: string;                 // Optional — Free-text notes
}
```

### 5.2 Status Display Config — create `src/config/statuses.ts`

```typescript
import { ApplicationStatus } from "../types";

export interface StatusConfig {
  label: string;
  emoji: string;
  color: string;       // Tailwind text color class
  bgColor: string;     // Tailwind background color class
}

export const STATUS_CONFIG: Record<ApplicationStatus, StatusConfig> = {
  [ApplicationStatus.Saved]:       { label: "Saved",       emoji: "📌", color: "text-gray-400",   bgColor: "bg-gray-400/10" },
  [ApplicationStatus.Applied]:     { label: "Applied",     emoji: "📤", color: "text-blue-400",   bgColor: "bg-blue-400/10" },
  [ApplicationStatus.InReview]:    { label: "In Review",   emoji: "👀", color: "text-yellow-400", bgColor: "bg-yellow-400/10" },
  [ApplicationStatus.PhoneScreen]: { label: "Phone Screen",emoji: "📞", color: "text-cyan-400",   bgColor: "bg-cyan-400/10" },
  [ApplicationStatus.Interview]:   { label: "Interview",   emoji: "🎤", color: "text-purple-400", bgColor: "bg-purple-400/10" },
  [ApplicationStatus.Technical]:   { label: "Technical",   emoji: "💻", color: "text-indigo-400", bgColor: "bg-indigo-400/10" },
  [ApplicationStatus.FinalRound]:  { label: "Final Round", emoji: "🏁", color: "text-orange-400", bgColor: "bg-orange-400/10" },
  [ApplicationStatus.Offer]:       { label: "Offer",       emoji: "🎉", color: "text-green-400",  bgColor: "bg-green-400/10" },
  [ApplicationStatus.Accepted]:    { label: "Accepted",    emoji: "✅", color: "text-emerald-400",bgColor: "bg-emerald-400/10" },
  [ApplicationStatus.Rejected]:    { label: "Rejected",    emoji: "❌", color: "text-red-400",    bgColor: "bg-red-400/10" },
  [ApplicationStatus.Withdrawn]:   { label: "Withdrawn",   emoji: "🚫", color: "text-slate-400",  bgColor: "bg-slate-400/10" },
};
```

---

## 6. Component Architecture

### 6.1 Component Tree

```mermaid
graph TD
    A["App"] --> B["Header"]
    A --> C["StatsBar"]
    A --> D["FilterBar"]
    A --> E["ApplicationList"]
    A --> F["ApplicationModal"]
    A --> G["ConfirmDialog"]
    E --> H["ApplicationCard"]
    F --> I["ApplicationForm"]
```

### 6.2 Components Breakdown

| Component | File | Responsibility |
|-----------|------|----------------|
| **App** | `src/App.tsx` | Root component. Holds state, renders layout. |
| **Header** | `src/components/Header.tsx` | App title + "Add New" button |
| **StatsBar** | `src/components/StatsBar.tsx` | Summary cards (total, interviews, offers, etc.) |
| **FilterBar** | `src/components/FilterBar.tsx` | Search input + status dropdown + sort selector |
| **ApplicationList** | `src/components/ApplicationList.tsx` | Maps over filtered apps, renders cards. Shows empty state. |
| **ApplicationCard** | `src/components/ApplicationCard.tsx` | Single application card with status badge, edit/delete buttons |
| **ApplicationModal** | `src/components/ApplicationModal.tsx` | Modal wrapper using `<dialog>`. Contains the form. |
| **ApplicationForm** | `src/components/ApplicationForm.tsx` | The actual form with inputs, validation, submit handler |
| **ConfirmDialog** | `src/components/ConfirmDialog.tsx` | "Are you sure?" confirmation for deletes |
| **StatusBadge** | `src/components/StatusBadge.tsx` | Reusable colored badge showing status emoji + label |

### 6.3 State Management

Use **React `useState`** — no Redux or external state library needed for this project.

State lives in `App.tsx`:
```typescript
const [applications, setApplications] = useState<Application[]>([]);
const [searchQuery, setSearchQuery] = useState("");
const [statusFilter, setStatusFilter] = useState<ApplicationStatus | "all">("all");
const [sortOrder, setSortOrder] = useState<"newest" | "oldest">("newest");
const [isModalOpen, setIsModalOpen] = useState(false);
const [editingApp, setEditingApp] = useState<Application | null>(null);
```

> [!TIP]
> **Custom Hook:** Extract localStorage logic into a `useLocalStorage` hook in `src/hooks/useLocalStorage.ts`. This makes it reusable and keeps `App.tsx` clean.

---

## 7. File Structure

```
applications-tracker/
├── index.html
├── package.json
├── tsconfig.json
├── vite.config.ts
├── PRD.md                          ← This document
├── README.md
└── src/
    ├── main.tsx                    ← React entry point
    ├── App.tsx                     ← Root component
    ├── index.css                   ← Tailwind import
    ├── types/
    │   └── index.ts                ← Application interface, enums
    ├── config/
    │   └── statuses.ts             ← Status display config (colors, emojis)
    ├── hooks/
    │   └── useLocalStorage.ts      ← Custom hook for localStorage
    ├── utils/
    │   └── helpers.ts              ← Date formatting, CSV export, etc.
    └── components/
        ├── Header.tsx
        ├── StatsBar.tsx
        ├── FilterBar.tsx
        ├── ApplicationList.tsx
        ├── ApplicationCard.tsx
        ├── ApplicationModal.tsx
        ├── ApplicationForm.tsx
        ├── ConfirmDialog.tsx
        └── StatusBadge.tsx
```

---

## 8. UI / UX Specifications

### 8.1 Page Layout

```
┌──────────────────────────────────────────────────┐
│  🔍 Applications Tracker              [+ Add New]│  ← Header
├──────────────────────────────────────────────────┤
│  Total: 24  │ Interviews: 5 │ Offers: 2 │ ...   │  ← StatsBar
├──────────────────────────────────────────────────┤
│  [Search... 🔍]  [Status ▼]  [Sort by Date ▼]   │  ← FilterBar
├──────────────────────────────────────────────────┤
│                                                  │
│  ┌────────────────────────────────────────────┐  │
│  │ Google  ·  Frontend Dev  ·  🇯🇵 Japan      │  │
│  │ Applied: Aug 1  ·  Status: 🎤 Interview   │  │  ← ApplicationCard
│  │ [Edit] [Delete]                            │  │
│  └────────────────────────────────────────────┘  │
│                                                  │
│  ┌────────────────────────────────────────────┐  │
│  │ Amazon  ·  SDE II  ·  🇺🇸 USA              │  │
│  │ Applied: Jul 28  ·  Status: ❌ Rejected    │  │  ← ApplicationCard
│  │ [Edit] [Delete]                            │  │
│  └────────────────────────────────────────────┘  │
│                                                  │
├──────────────────────────────────────────────────┤
│  Applications Tracker · Data stored locally      │  ← Footer
└──────────────────────────────────────────────────┘
```

### 8.2 Add/Edit Modal

```
┌─────────────── Add Application ───────────────┐
│                                               │
│  Company Name *    [___________________]      │
│  Position *        [___________________]      │
│  Application URL   [___________________]      │
│  Country           [___________________]      │
│  Location          [___________________]      │
│  Status *          [Applied         ▼]        │
│  Date Applied *    [2026-08-05      📅]       │
│  Salary Range      [___________________]      │
│  Contact Person    [___________________]      │
│  Notes             [___________________]      │
│                    [___________________]      │
│                                               │
│           [Cancel]          [Save]            │
└───────────────────────────────────────────────┘
```

### 8.3 Design Guidelines

| Aspect | Guideline |
|--------|-----------|
| **Theme** | Dark mode default — `bg-gray-950` body, `bg-gray-900` cards |
| **Font** | Use [Inter](https://fonts.google.com/specimen/Inter) via Google Fonts |
| **Accent Color** | Blue-violet gradient (`from-blue-500 to-violet-500`) |
| **Status Badges** | Colored pill badges using the `StatusConfig` mapping |
| **Responsiveness** | Mobile-first — cards stack vertically on small screens |
| **Animations** | Use Tailwind's `transition`, `hover:scale-[1.02]`, `animate-fade-in` |
| **Empty State** | Friendly illustration/message when no applications exist |
| **Border Radius** | `rounded-xl` for cards, `rounded-lg` for inputs |
| **Spacing** | Consistent `p-4` / `p-6` padding, `gap-4` between cards |

### 8.4 Tailwind Color Reference

```
Background:   bg-gray-950 (page), bg-gray-900 (cards), bg-gray-800 (inputs)
Text:         text-white (headings), text-gray-300 (body), text-gray-500 (muted)
Accent:       blue-500, violet-500 (buttons, links, highlights)
Borders:      border-gray-700/50 (subtle dividers)
```

---

## 9. Key React Patterns to Learn

### 9.1 Custom Hook — `useLocalStorage`

```typescript
// src/hooks/useLocalStorage.ts
import { useState, useEffect } from "react";

export function useLocalStorage<T>(key: string, initialValue: T) {
  const [value, setValue] = useState<T>(() => {
    const stored = localStorage.getItem(key);
    return stored ? JSON.parse(stored) : initialValue;
  });

  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);

  return [value, setValue] as const;
}
```

### 9.2 Passing Props

```typescript
// Parent passes data + callbacks down to children
<ApplicationCard
  application={app}
  onEdit={(app) => openEditModal(app)}
  onDelete={(id) => handleDelete(id)}
/>
```

### 9.3 Conditional Rendering

```tsx
{applications.length === 0 ? (
  <EmptyState />
) : (
  applications.map(app => <ApplicationCard key={app.id} application={app} />)
)}
```

### 9.4 Form Handling

```tsx
const [formData, setFormData] = useState<Partial<Application>>({});

const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
  setFormData(prev => ({ ...prev, [e.target.name]: e.target.value }));
};
```

> [!NOTE]
> These are patterns to study and use — not copy-paste solutions. Understand **why** each pattern works.

---

## 10. One-Week Schedule

Each day follows the same rhythm: **branch → code → commit → push → PR → merge**.

| Day | Branch | Focus | Deliverables | PR |
|-----|--------|-------|-------------|----|
| **Day 1** | `day-1/project-setup` | **Setup & Learn** | Initialize Vite+React+TS+Tailwind (Section 3). Get dev server running. Read React docs: [Quick Start](https://react.dev/learn). Build a "Hello World" component. | PR #1: "Day 1: Project Setup" |
| **Day 2** | `day-2/types-and-layout` | **Types & Layout** | Create TypeScript types (Section 5). Build `Header`, `StatsBar` (static), `Footer`. Style with Tailwind dark theme. | PR #2: "Day 2: Types & Layout" |
| **Day 3** | `day-3/storage-and-data` | **Storage & Data** | Build `useLocalStorage` hook. Create add/edit/delete helpers. Wire up `App.tsx` state. Test with dummy data. | PR #3: "Day 3: Storage & Data" |
| **Day 4** | `day-4/form-and-modal` | **Form & Modal** | Build `ApplicationModal` + `ApplicationForm`. Handle submit — add new apps. Display with `ApplicationList` + `ApplicationCard`. | PR #4: "Day 4: Form & Modal" |
| **Day 5** | `day-5/edit-delete-status` | **Edit, Delete & Status** | Implement edit (pre-fill form), delete (`ConfirmDialog`), status updates. Build `StatusBadge`. | PR #5: "Day 5: Edit, Delete & Status" |
| **Day 6** | `day-6/search-filter-polish` | **Search, Filter & Polish** | Add `FilterBar` — search, status filter, sort. Dynamic `StatsBar`. Empty state, animations, responsive. | PR #6: "Day 6: Search & Polish" |
| **Day 7** | `day-7/deploy-and-readme` | **Deploy & README** | `npm run deploy` to GitHub Pages. Write README with screenshots. Test on mobile. Final fixes. | PR #7: "Day 7: Deploy & Docs" |

> [!NOTE]
> **End-of-day checklist:**
> 1. All changes committed with descriptive messages
> 2. Branch pushed to GitHub
> 3. PR created with a title and short description
> 4. PR merged to `main`
> 5. Locally: `git checkout main && git pull`

---

## 11. Learning Objectives

By the end of this project, you will have practiced:

- [ ] **React** — Components, props, state, hooks, event handling, conditional rendering
- [ ] **TypeScript** — Interfaces, enums, type annotations, generics
- [ ] **Tailwind CSS** — Utility classes, responsive design, dark mode, transitions
- [ ] **Vite** — Dev server, builds, plugins, configuration
- [ ] **Custom Hooks** — Extracting reusable logic (`useLocalStorage`)
- [ ] **CRUD Operations** — Create, Read, Update, Delete with local storage
- [ ] **Git Workflow** — Branching, pull requests, merging, commit message conventions
- [ ] **Deployment** — GitHub Pages with Vite

---

## 12. Helpful Resources

| Topic | Resource |
|-------|----------|
| React Quick Start | [react.dev/learn](https://react.dev/learn) |
| React Hooks | [react.dev/reference/react/hooks](https://react.dev/reference/react/hooks) |
| TypeScript Handbook | [typescriptlang.org/docs/handbook](https://www.typescriptlang.org/docs/handbook/) |
| Tailwind CSS Docs | [tailwindcss.com/docs](https://tailwindcss.com/docs) |
| Vite Guide | [vite.dev/guide](https://vite.dev/guide/) |
| HTML `<dialog>` | [MDN: dialog element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dialog) |
| Google Fonts (Inter) | [fonts.google.com/specimen/Inter](https://fonts.google.com/specimen/Inter) |
| GitHub Pages + Vite | [vite.dev/guide/static-deploy#github-pages](https://vite.dev/guide/static-deploy#github-pages) |
| Git basics | [git-scm.com/book](https://git-scm.com/book/en/v2) |

---

## 13. Acceptance Criteria (Definition of Done)

The project is **done** when:

- [ ] User can **add** a new job application via a modal form
- [ ] User can **view** all applications as cards
- [ ] User can **edit** an existing application
- [ ] User can **delete** an application (with confirmation)
- [ ] User can **filter** applications by status
- [ ] User can **search** by company name or position
- [ ] Data **persists** after page refresh (localStorage)
- [ ] The app is **deployed** and accessible on GitHub Pages
- [ ] The app is **responsive** (works on mobile)
- [ ] The app looks **polished and modern** (dark theme, smooth transitions)
- [ ] Code uses **TypeScript** with proper types — no `any`
- [ ] Components are **well-structured** and reusable

---

> [!IMPORTANT]
> **Don't just copy the code snippets** in this PRD. Type them out, understand what each line does, and experiment by changing things. That's how you actually learn.

> **Good luck! Build something you'd actually want to use.** 🚀
