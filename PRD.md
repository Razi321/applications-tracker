# 📋 Applications Tracker — Product Requirements Document (PRD)

> **Author:** Razi  
> **Date:** August 5, 2026  
> **Duration:** 1-week side project  
> **Audience:** Junior developer (learning project)  
> **Repository:** [Razi321/applications-tracker](https://github.com/Razi321/applications-tracker)

---

## 1. Product Overview

### What is it?
A **single-page web application** that helps job seekers track their job applications in one place — replacing messy spreadsheets with a clean, modern UI.

### Why build it?
- People use Excel/Google Sheets to track applications — it works but it's ugly and hard to filter
- A dedicated UI makes it faster to add, update, and visualize application status
- It's a great learning project that covers **HTML, CSS, JavaScript, data modeling, and deployment**

### Who is it for?
Anyone actively applying for jobs who wants a simple, free, private tracker that runs in their browser.

---

## 2. Tech Stack

| Layer | Technology | Why |
|-------|-----------|-----|
| **Structure** | HTML5 | Semantic markup, forms, dialogs |
| **Styling** | Vanilla CSS | Learn CSS properly — no frameworks as a crutch |
| **Logic** | Vanilla JavaScript (ES6+) | DOM manipulation, event handling, data management |
| **Storage** | `localStorage` | Free, no backend needed, data stays in the browser |
| **Hosting** | GitHub Pages | Free static hosting, deploys from the repo |
| **Version Control** | Git + GitHub | Track progress, learn git workflow |

### What you will NOT need
- ❌ No React, Vue, or Angular
- ❌ No Node.js or npm
- ❌ No database or backend server
- ❌ No paid hosting or services
- ❌ No CSS frameworks (no Tailwind, no Bootstrap)

> [!IMPORTANT]
> **Everything is free. Everything runs in the browser. No accounts or API keys needed.**

---

## 3. Features

### 3.1 Core Features (Must Have)

| # | Feature | Description |
|---|---------|-------------|
| F1 | **Add Application** | A form/modal to add a new job application with all fields |
| F2 | **View Applications** | A table/card list showing all tracked applications |
| F3 | **Edit Application** | Click on an application to update its details |
| F4 | **Delete Application** | Remove an application with a confirmation prompt |
| F5 | **Status Tracking** | Update application status through predefined stages |
| F6 | **Persistent Storage** | Data saved in `localStorage` — survives page refresh |
| F7 | **Search & Filter** | Filter by status, search by company name or position |

### 3.2 Nice-to-Have Features (If Time Permits)

| # | Feature | Description |
|---|---------|-------------|
| N1 | **Dashboard Stats** | Summary cards: total apps, interviews, offers, rejections |
| N2 | **Sort by Date** | Sort applications by date applied (newest/oldest first) |
| N3 | **Export to CSV** | Download all data as a `.csv` file |
| N4 | **Import from CSV** | Upload a `.csv` to bulk-add applications |
| N5 | **Dark Mode Toggle** | Switch between light and dark themes |
| N6 | **Color-coded Status** | Each status gets a distinct color badge |

---

## 4. Data Model

Each application is a **JavaScript object** stored in a `localStorage` array.

### Application Object

```javascript
{
  id: "uuid-string",           // Unique identifier (use crypto.randomUUID())
  companyName: "Google",       // Required — Company name
  position: "Frontend Dev",    // Required — Job title / role
  applicationUrl: "https://...", // Optional — Link to the job posting
  country: "Japan",            // Optional — Country of the job
  location: "Tokyo",           // Optional — City or "Remote"
  status: "applied",           // Required — Current status (see below)
  dateApplied: "2026-08-01",   // Required — When you applied (YYYY-MM-DD)
  dateUpdated: "2026-08-05",   // Auto-set — Last modification date
  salary: "¥8M - ¥10M",       // Optional — Salary range
  contactPerson: "Jane Doe",   // Optional — Recruiter / contact name
  notes: "Had a great call..." // Optional — Free-text notes
}
```

### Status Values (Enum)

```
saved        → 📌 Saved (bookmarked, not yet applied)
applied      → 📤 Applied (application submitted)
in_review    → 👀 In Review (application being reviewed)
phone_screen → 📞 Phone Screen (initial phone call)
interview    → 🎤 Interview (formal interview stage)
technical    → 💻 Technical Assessment (coding test / take-home)
final_round  → 🏁 Final Round (last interview stage)
offer        → 🎉 Offer Received
accepted     → ✅ Accepted
rejected     → ❌ Rejected
withdrawn    → 🚫 Withdrawn (you pulled out)
```

> [!TIP]
> Store these statuses as an array constant so the UI dropdowns and filters can reference one source of truth.

---

## 5. UI / UX Specifications

### 5.1 Page Layout (Single Page)

```
┌──────────────────────────────────────────────────┐
│  🔍 Applications Tracker              [+ Add New]│  ← Header
├──────────────────────────────────────────────────┤
│  Total: 24  │ Interviews: 5 │ Offers: 2 │ ...   │  ← Stats Bar (N1)
├──────────────────────────────────────────────────┤
│  [Search... 🔍]  [Status ▼]  [Sort by Date ▼]   │  ← Filters Bar
├──────────────────────────────────────────────────┤
│                                                  │
│  ┌────────────────────────────────────────────┐  │
│  │ Google  ·  Frontend Dev  ·  🇯🇵 Japan      │  │
│  │ Applied: Aug 1  ·  Status: 🎤 Interview   │  │  ← Application Card
│  │ [Edit] [Delete]                            │  │
│  └────────────────────────────────────────────┘  │
│                                                  │
│  ┌────────────────────────────────────────────┐  │
│  │ Amazon  ·  SDE II  ·  🇺🇸 USA              │  │
│  │ Applied: Jul 28  ·  Status: ❌ Rejected    │  │  ← Application Card
│  │ [Edit] [Delete]                            │  │
│  └────────────────────────────────────────────┘  │
│                                                  │
│  ... more cards ...                              │
│                                                  │
├──────────────────────────────────────────────────┤
│  Applications Tracker · Data stored locally      │  ← Footer
└──────────────────────────────────────────────────┘
```

### 5.2 Add/Edit Modal

When clicking **"+ Add New"** or **"Edit"**, a modal dialog opens:

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

> [!NOTE]
> Fields marked with `*` are required. The modal should use the native `<dialog>` HTML element.

### 5.3 Design Guidelines

| Aspect | Guideline |
|--------|-----------|
| **Theme** | Dark mode preferred (easier on eyes, looks modern) |
| **Font** | Use [Inter](https://fonts.google.com/specimen/Inter) from Google Fonts |
| **Colors** | Use a cohesive palette — suggest dark grays + accent color (blue or purple) |
| **Status Badges** | Each status gets a unique color (green = offer, red = rejected, etc.) |
| **Responsiveness** | Must work on desktop AND mobile (use CSS media queries) |
| **Animations** | Subtle transitions on hover, modal open/close |
| **Empty State** | Show a friendly message when no applications exist yet |

---

## 6. File Structure

```
applications-tracker/
├── index.html          ← Main HTML page
├── css/
│   └── style.css       ← All styles
├── js/
│   ├── app.js          ← Main app logic (init, render, event listeners)
│   ├── storage.js      ← localStorage read/write helpers
│   └── utils.js        ← Utility functions (ID generation, date formatting)
├── assets/
│   └── favicon.ico     ← Optional favicon
└── README.md           ← Project description
```

> [!TIP]
> Keep it simple. 3 JS files max. Don't over-engineer the folder structure.

---

## 7. localStorage API Reference

Here's a quick cheat-sheet for working with `localStorage`:

```javascript
// Save data
const apps = [{ id: "1", companyName: "Google", ... }];
localStorage.setItem("applications", JSON.stringify(apps));

// Load data
const apps = JSON.parse(localStorage.getItem("applications")) || [];

// Delete all data
localStorage.removeItem("applications");
```

> [!CAUTION]
> `localStorage` has a ~5MB limit. More than enough for thousands of applications, but don't store images or large files in it.

---

## 8. Deployment to GitHub Pages

### Steps:
1. Push all your code to the `main` branch
2. Go to the repo → **Settings** → **Pages**
3. Under "Source", select **Deploy from a branch**
4. Choose `main` branch and `/ (root)` folder
5. Click **Save**
6. Your site will be live at: `https://razi321.github.io/applications-tracker/`

> [!NOTE]
> It takes 1-2 minutes for GitHub Pages to deploy after pushing. The URL is free and permanent.

---

## 9. One-Week Schedule

| Day | Focus | Deliverables |
|-----|-------|-------------|
| **Day 1** | **Setup & HTML** | Set up the repo locally. Write `index.html` with semantic structure: header, main content area, footer, and the `<dialog>` modal. No styling yet — just the skeleton. |
| **Day 2** | **CSS & Design** | Create `style.css`. Implement the dark theme, layout (CSS Grid or Flexbox), card styles, status badges, and responsive design. Make it look great. |
| **Day 3** | **JavaScript — Storage** | Write `storage.js` with functions: `getApplications()`, `saveApplication(app)`, `deleteApplication(id)`, `updateApplication(id, data)`. Test in the browser console. |
| **Day 4** | **JavaScript — UI Logic** | Write `app.js`. Wire up the form, render cards dynamically, handle add/edit/delete with event listeners. Connect to storage. |
| **Day 5** | **Search, Filter & Sort** | Add the search bar (filter by company/position), status dropdown filter, and date sorting. |
| **Day 6** | **Polish & Nice-to-Haves** | Add stats dashboard, empty state, animations, CSV export, and any remaining nice-to-haves. Fix bugs. |
| **Day 7** | **Deploy & README** | Deploy to GitHub Pages. Write a proper README with screenshots. Test on mobile. Final cleanup. |

---

## 10. Learning Objectives

By the end of this project, you will have practiced:

- [x] **HTML5** — Semantic elements, forms, `<dialog>`, accessibility
- [x] **CSS** — Flexbox/Grid layout, custom properties, media queries, transitions, dark themes
- [x] **JavaScript** — DOM manipulation, event handling, `localStorage`, array methods (`filter`, `map`, `sort`), template literals
- [x] **Git** — `add`, `commit`, `push`, branching basics
- [x] **Deployment** — GitHub Pages (static site hosting)
- [x] **Data Modeling** — Designing a schema, CRUD operations
- [x] **UX Thinking** — Empty states, confirmations, responsive design

---

## 11. Helpful Resources

| Topic | Resource |
|-------|----------|
| HTML `<dialog>` | [MDN: dialog element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dialog) |
| CSS Flexbox | [CSS Tricks: Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) |
| CSS Grid | [CSS Tricks: Grid Guide](https://css-tricks.com/snippets/css/complete-guide-grid/) |
| localStorage | [MDN: Web Storage API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API) |
| Google Fonts (Inter) | [fonts.google.com/specimen/Inter](https://fonts.google.com/specimen/Inter) |
| GitHub Pages | [docs.github.com/pages](https://docs.github.com/en/pages) |
| Git basics | [git-scm.com/book](https://git-scm.com/book/en/v2) |
| `crypto.randomUUID()` | [MDN: randomUUID](https://developer.mozilla.org/en-US/docs/Web/API/Crypto/randomUUID) |

---

## 12. Acceptance Criteria (Definition of Done)

The project is **done** when:

- [ ] User can **add** a new job application via a modal form
- [ ] User can **view** all applications as cards/rows
- [ ] User can **edit** an existing application
- [ ] User can **delete** an application (with confirmation)
- [ ] User can **filter** applications by status
- [ ] User can **search** by company name or position
- [ ] Data **persists** after page refresh (localStorage)
- [ ] The app is **deployed** and accessible on GitHub Pages
- [ ] The app is **responsive** (works on mobile)
- [ ] The app looks **polished and modern** (not like a homework assignment)

---

> **Good luck! Build something you'd actually want to use.** 🚀
