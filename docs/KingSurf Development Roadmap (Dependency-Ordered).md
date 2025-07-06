# KingSurf Development Roadmap (Dependency-Ordered)

## 🎯 CURRENT STATUS (Updated June 2025)

### ✅ Major Accomplishments
- **Browser Fork & Branding**: Forked Gecko, replaced names/icons with KingSurf branding
- **Build System**: macOS arm64 build pipeline in place; CI for macOS builds
- **Custom Homepage & Defaults**: about:kingsurf and privacy-focused preferences
- **Vertical Tab Sidebar & Theming MVP**: Collapsible sidebar, auto-hide, compact mode, dark/light themes, accessibility basics
- **Testing Infrastructure**: Basic test harness set up for branding and vertical tabs

### 🚀 Immediate Next Priorities
1. Stage 4: Quality & Testing for Vertical Tabs & Theming
2. Stage 5: Distribution Prep (Windows/Linux pipelines, update server, privacy policy)
3. Stage 6: MVP Launch (vertical tabs & theming)
4. Stage 7: Core Feature Implementation (full consolidated feature set)
5. Stage 8: Sync & Mobile Shells
6. Stage 9: Post-Core Enhancements & Monitoring

---

## Stage 1: Foundation ✅
- [x] 1.1 Define Browser Concept & Goals  
- [x] 1.2 Set Up Development Workflow (build system, automated tests, CI/CD, docs)

## Stage 2: Basic Identity ✅
- [x] 2.1 Replace original branding with KingSurf
- [x] 2.2 Custom default preferences and homepage (about:kingsurf)
- [x] 2.3 Disable upstream telemetry
- [x] 2.4 Integrate logo and icon assets

## Stage 3: Core Feature MVP (Vertical Tabs & Theming) ✅
- [x] 3.1 Collapsible Vertical Tab Sidebar (CSS/JS, toggle, shortcut)
- [x] 3.2 Auto-hide on hover (Compact Mode)
- [x] 3.3 Compact mode styling (icon-only, tooltips)
- [x] 3.4 Basic Theming Engine (dark/light, CSS variables, responsiveness, accessibility)
- [x] 3.5 Initial tests for these features

---

## Stage 4: Quality & Testing for Vertical Tabs & Theming
*(Requires Stage 3 complete)*

- [ ] 4.1 Automated UI Tests for Vertical Tabs  
  - Write Marionette/Browser Toolbox tests verifying expand/collapse, auto-hide, compact toggle, keyboard shortcuts.  
  - CI: add `ui-tests-vertical-tabs` job.  
- [ ] 4.2 Performance Benchmarking  
  - Scripts measuring startup time, tab-switch latency, memory footprint with sidebar active.  
  - CI: add benchmark job.  
- [ ] 4.3 Memory Usage Validation  
  - Automated memory-regression checks.  
- [ ] 4.4 Cross-Site Compatibility Testing  
  - Smoke tests on popular sites to catch rendering or extension breakages.

---

## Stage 5: Distribution Prep
*(Requires Stage 4 passing tests and benchmarks)*

- [ ] 5.1 Code Signing Setup  
  - Windows NSIS signing; Linux checksums/signing; macOS already done.  
- [ ] 5.2 Installer Packaging for Windows & Linux  
  - Build and test installers on clean environments.  
- [ ] 5.3 Update Server & Configuration  
  - Minimal update server hosting manifests/MARs; prefs in `defaults/pref/` pointing to update URL.  
- [ ] 5.4 Legal & Privacy Policy Draft  
  - Privacy policy covering upcoming AI features and data flows; integrate consent UI.

---

## Stage 6: MVP Launch (Vertical Tabs & Theming)
*(Requires Stage 5 complete)*

- [ ] 6.1 Beta Testing  
  - Distribute to testers, gather stability/UX feedback.  
- [ ] 6.2 Feedback Iteration  
  - Fix critical issues, refine sidebar UX.  
- [ ] 6.3 Release Preparation  
  - Finalize version, release notes, docs, landing page update.  
- [ ] 6.4 Public Release  
  - Publish installers/update metadata; open feedback channels.

---

## Stage 7: Core Feature Implementation (Post-MVP)
*(Requires Stage 6 stable release)*

### 7.1 Settings & Infrastructure Prerequisites
These provide foundational settings and consent needed by many features.

- [ ] 7.1.1 AI & Privacy Settings UI  
  - **Description**: Add preferences pane entries for AI endpoint configuration, opt-in consent, privacy toggles.  
  - **Dependencies**: Stage 5 privacy policy.  
  - **Deliverables**: Settings UI code under `browser/base/content/preferences/`.  
  - **AI Prompt**: “Generate settings UI code for KingSurf to input AI endpoint URL, toggle AI features, and configure privacy consent.”
- [ ] 7.1.2 Secure Data Handling & Sync Preparation  
  - **Description**: Design data flow for AI interactions and prepare for encrypted sync of notes/workspaces.  
  - **Dependencies**: 7.1.1 settings in place.  
  - **Deliverables**: Encryption/key management design; placeholder storage modules.  
  - **AI Prompt**: “Write pseudocode for encrypting/decrypting JSON payloads (notes, workspaces) for later sync in KingSurf.”

### 7.2 Intelligent UI & Navigation Features
These depend only on sidebar/theming infrastructure.

- [ ] 7.2.1 Workspace Groups / Tab Groups  
  - **Description**: Named sets of tabs/windows; isolate contexts.  
  - **Dependencies**: Sidebar infrastructure (Stage 3).  
  - **Deliverables**: UX mockup; data model; prototype (built-in extension or native patch).  
  - **AI Prompts**: 
    - “Generate manifest.json and stub JS for a KingSurf extension managing named workspaces via browser.tabs/windows APIs.”  
    - “Define a data structure for storing workspaces mapping names to tab lists and window IDs.”  
- [ ] 7.2.2 Split-Screen Tiling  
  - **Description**: Tile pages side-by-side in one window.  
  - **Dependencies**: Tab management system.  
  - **Deliverables**: CSS/JS for split layout, resize controls, keyboard shortcuts.  
  - **AI Prompt**: “Write CSS and JS stubs to split the content area into two resizable panes showing different tabs in KingSurf.”  
- [ ] 7.2.3 Quick-Peek Overlays  
  - **Description**: Lightweight previews for links/definitions/media without full tab switch.  
  - **Dependencies**: Overlay framework in UI.  
  - **Deliverables**: Overlay component code, dismissal logic.  
  - **AI Prompt**: “Provide JS/CSS for opening a modal overlay that loads a preview of a link in a sandboxed iframe, with close behavior.”  
- [ ] 7.2.4 Tab Timeline & Visual History  
  - **Description**: Sidebar timeline showing thumbnails of visited pages with timestamps.  
  - **Dependencies**: Access to tab opening and history events.  
  - **Deliverables**: UI panel; snapshot capture logic; reopen action.  
  - **AI Prompts**: 
    - “Generate JS/CSS for a sidebar timeline panel displaying thumbnail snapshots of recently visited pages with timestamps and click-to-reopen functionality.”  
    - “Write code to capture page thumbnails when tabs open or at intervals.”  
- [ ] 7.2.5 Testing UI & Navigation  
  - **Description**: Automated UI tests for workspace switching, split view, quick-peek, timeline.  
  - **Dependencies**: 7.2.1–7.2.4 prototypes complete.  
  - **Deliverables**: Marionette/Browser Toolbox tests; CI job `ui-tests-navigation`.  
  - **AI Prompt**: “Write a Marionette test for workspace switching: open tabs in two workspaces, switch, verify visibility.”

### 7.3 Deep AI Assistance Features
Require settings from 7.1.

- [ ] 7.3.1 Conversational Command Bar  
  - **Description**: Natural-language input for actions (“Summarize page”, “Open workspace X”).  
  - **Dependencies**: 7.1.1 settings UI.  
  - **Deliverables**: Input UI, command parser stub, dispatcher.  
  - **AI Prompt**: “Provide JS stub for parsing natural-language commands in KingSurf and invoking corresponding functions.”  
- [ ] 7.3.2 On-Page Summarization & Note Capture  
  - **Description**: Sidebar panel sends page content/selection to AI endpoint; displays summary and editable notes.  
  - **Dependencies**: 7.3.1; 7.1.1 for endpoint config.  
  - **Deliverables**: Sidebar UI code; network request handling; storage of notes (encrypted if sync enabled).  
  - **AI Prompt**: “Write JS for a sidebar panel that sends page content to a configured AI endpoint and displays the returned summary with an editable note field.”  
- [ ] 7.3.3 Automated Workflows  
  - **Description**: Define multi-step routines via natural language (e.g., collect links, summarize, export).  
  - **Dependencies**: 7.3.1 and 7.3.2.  
  - **Deliverables**: Workflow definition UI; execution engine invoking AI/browser actions step-by-step with confirmation.  
  - **AI Prompt**: “Generate a UI and JS pseudocode for defining and executing a sequence of browser actions with AI integration in KingSurf.”  
- [ ] 7.3.4 Contextual Recommendations  
  - **Description**: AI suggests related resources/tutorials based on page content.  
  - **Dependencies**: 7.3.2.  
  - **Deliverables**: Sidebar panel; network integration to AI endpoint.  
  - **AI Prompt**: “Write code to send page keywords to AI endpoint and render suggested links or actions in a side panel.”  
- [ ] 7.3.5 AI-Powered Whiteboard & Brainstorming  
  - **Description**: Integrated canvas with freehand drawing; AI analyzes sketch/text to refine diagrams or suggest next steps.  
  - **Dependencies**: 7.1.1 settings; 7.3.1 UI framework.  
  - **Deliverables**: Canvas component; drawing tools; AI integration for suggestions overlay.  
  - **AI Prompt**: “Generate code for a browser-integrated whiteboard panel allowing freehand drawing and sending drawing description to an AI endpoint for suggestions.”  
- [ ] 7.3.6 Testing AI Helpers  
  - **Description**: Mock AI responses; verify UI behavior for summarization, workflows, whiteboard.  
  - **Dependencies**: 7.3.1–7.3.5 implemented.  
  - **Deliverables**: Automated tests with stubbed AI; manual test cases.  
  - **AI Prompt**: “Generate a test harness simulating AI endpoint responses and verifying summarization sidebar displays correct content.”

### 7.4 Privacy & Security Features
Require settings from 7.1.

- [ ] 7.4.1 Live Privacy Dashboard  
  - **Description**: Panel showing trackers blocked, third-party requests, Privacy Score with AI guidance.  
  - **Dependencies**: 7.1.1 settings; network observer hook.  
  - **Deliverables**: Observer code; UI panel; toggle controls.  
  - **AI Prompt**: “Write CSS/JS for a privacy dashboard panel listing tracker counts and cookie blocks, with AI-generated advice.”  
- [ ] 7.4.2 Permission Management with AI Guidance  
  - **Description**: On permission prompts, show AI explanation of risks/benefits.  
  - **Dependencies**: 7.4.1; 7.1.1 settings.  
  - **Deliverables**: Hook into permission UI; call AI endpoint; display guidance.  
  - **AI Prompt**: “Provide code stub to intercept permission requests and fetch a natural-language explanation from AI based on site context.”  
- [ ] 7.4.3 Phishing & Malicious Site Alerts  
  - **Description**: Check URLs against safe-browsing lists plus AI heuristics; warn with explanations.  
  - **Dependencies**: network observer infrastructure; 7.1.1 settings.  
  - **Deliverables**: URL check logic; AI analysis stub; warning UI.  
  - **AI Prompt**: “Write code to check current URL against a safe-browsing list and use AI to generate an explanation if flagged, then show warning.”  
- [ ] 7.4.4 Testing Privacy & Security  
  - **Description**: Automated tests simulating network events and permission flows; manual QA for alerts/guidance.  
  - **Dependencies**: 7.4.1–7.4.3 implemented.  
  - **Deliverables**: Test scripts; QA checklist.  
  - **CI Adjustments**: Add privacy/security test jobs.

### 7.5 Productivity & Focus Features
Depend on Workspaces (7.2.1) and AI helpers (7.3).

- [ ] 7.5.1 Focus Mode  
  - **Description**: Distraction-blocking: hide/dim non-essential elements; whitelist-only browsing for timed sessions.  
  - **Dependencies**: UI injection framework; 7.1.1 settings.  
  - **Deliverables**: Toggle UI; CSS injection logic; timer overlay; whitelist settings.  
  - **AI Prompt**: “Write JS/CSS to apply focus mode style hiding non-essential page elements and a countdown timer overlay.”  
- [ ] 7.5.2 Smart Tab Sleeping  
  - **Description**: Automatically suspend inactive tabs based on rules/AI predictions; wake on demand.  
  - **Dependencies**: Core tab management; optional AI integration from 7.3.2.  
  - **Deliverables**: Inactivity detection; suspend/resume logic; suggestion UI.  
  - **AI Prompt**: “Write JS pseudocode for detecting inactive tabs in KingSurf and unloading content after timeout, with a sidebar suggestion list.”  
- [ ] 7.5.3 Session & Workspace Snapshots  
  - **Description**: Save/restore workspace state (tabs, scroll positions, form data).  
  - **Dependencies**: Workspaces implemented; tab sleeping logic helpful.  
  - **Deliverables**: Snapshot save/load; UI to manage snapshots.  
  - **AI Prompt**: “Provide code to capture workspace state (URLs, scroll) and restore it later, handling errors.”  
- [ ] 7.5.4 Integrated Task List  
  - **Description**: To-do list tied to workspaces; AI suggests subtasks.  
  - **Dependencies**: Workspaces (7.2.1) and AI helpers (7.3).  
  - **Deliverables**: Sidebar task panel; storage per workspace; AI suggestion integration.  
  - **AI Prompt**: “Generate JS for a sidebar task list component keyed by workspace with AI subtask suggestions.”  
- [ ] 7.5.5 Testing Productivity Features  
  - **Description**: Automated/manual tests for focus mode, tab sleeping, snapshots, task list.  
  - **Dependencies**: 7.5.1–7.5.4 implemented.  
  - **Deliverables**: Test scripts; QA checklist.  
  - **CI Adjustments**: Add jobs for memory regression and UI behavior under focus mode.

### 7.6 Customization & Accessibility
Can proceed once basic UI exists.

- [ ] 7.6.1 Theming Engine & Runtime Switching  
  - **Description**: Runtime theme changes without restart.  
  - **Dependencies**: Basic theming in Stage 3.  
  - **Deliverables**: Theme manager UI; CSS/JS integration.  
  - **AI Prompt**: “Generate JS to toggle CSS variable sets at runtime to switch themes.”  
- [ ] 7.6.2 Per-Site Styles  
  - **Description**: Custom CSS overrides per domain at page load.  
  - **Dependencies**: 7.6.1.  
  - **Deliverables**: UI for overrides; injection logic.  
  - **AI Prompt**: “Write code to inject user-provided CSS into pages matching domain patterns.”  
- [ ] 7.6.3 Adjustable UI Density & Accessibility Enhancements  
  - **Description**: Compact/spacious layouts; screen-reader optimizations; AI alt-text generation.  
  - **Dependencies**: UI framework.  
  - **Deliverables**: Settings for density; accessibility improvements; AI alt-text stub.  
  - **AI Prompt**: “Generate CSS/JS to adjust toolbar padding/font sizes based on density setting and detect missing alt attributes for AI generation.”

### 7.7 Communication & Integration
Requires sync backend.

- [ ] 7.7.1 Built-In Messaging Panel  
  - **Description**: Sidebar integrating with chat/collab services.  
  - **Dependencies**: Sync backend (Stage 8).  
  - **Deliverables**: UI stub; integration plan.  
  - **AI Prompt**: “Generate UI stub for a messaging sidebar with placeholders for external chat API integration.”  
- [ ] 7.7.2 Bookmark & History Insights  
  - **Description**: AI analyzes patterns to suggest bookmark grouping and resurface pages.  
  - **Dependencies**: AI helpers (7.3) and opt-in telemetry (Stage 9).  
  - **Deliverables**: Analysis module; UI for suggestions.  
  - **AI Prompt**: “Write pseudocode for analyzing browsing history data to recommend bookmark grouping and surface relevant pages.”  
- [ ] 7.7.3 Sync Across Desktop Instances  
  - **Description**: Encrypted sync of workspaces, notes, settings between desktops.  
  - **Dependencies**: Sync backend (Stage 8).  
  - **Deliverables**: Sync protocol design; initial implementation.  
  - **AI Prompt**: “Generate design for end-to-end encrypted sync of JSON data between KingSurf instances.”

### 7.8 Privacy & Security Revisited (advanced hooks)
Some parts built earlier; advanced integration now.

- [ ] 7.8.1 Enhance Privacy Dashboard with AI guidance (if not fully covered)  
  - **Description**: Extend dashboard recommendations with richer AI analytics.  
  - **Dependencies**: 7.4 live dashboard and AI helpers.  
  - **Deliverables**: Enhanced recommendation logic.  
  - **AI Prompt**: “Provide logic to refine Privacy Score using AI insights over historical data.”  
- [ ] 7.8.2 Permission Management Advanced Patterns  
  - **Description**: Context-aware permission rules (e.g., auto-deny risky patterns).  
  - **Dependencies**: 7.4.2 permission guidance.  
  - **Deliverables**: Rule engine and UI.  
  - **AI Prompt**: “Generate code to suggest permission defaults based on site reputation and user behavior patterns.”

---

## Stage 8: Sync & Mobile Shells Setup
*(Requires Stage 7.1 secure data handling and workspace implementation)*

- [ ] 8.1 Encrypted Sync Backend  
  - **Description**: Service or local-first design for encrypted sync of workspaces, notes, prefs.  
  - **Dependencies**: 7.1.2 design; 7.2 workspaces; 7.3 notes.  
  - **Deliverables**: Sync service prototype; encryption/key management code.  
  - **AI Prompt**: “Write pseudocode for encrypting/decrypting JSON payloads for sync with key management.”  
- [ ] 8.2 Android Shell App  
  - **Description**: WebView/GeckoView wrapper loading KingSurf UI where feasible; workspace/notes access.  
  - **Dependencies**: 8.1 sync backend.  
  - **Deliverables**: Android project scaffold; native workspace listing UI; summary sidebar stub.  
  - **AI Prompt**: “Generate an Android WebView app skeleton that loads a KingSurf URL and provides native UI to list/switch synced workspaces.”  
- [ ] 8.3 iOS Shell App  
  - **Description**: WKWebView-based iOS app with branding and basic workspace/summary access.  
  - **Dependencies**: 8.1 sync backend.  
  - **Deliverables**: Xcode project scaffold; UI for switching synced workspaces; summary feature stub.  
  - **AI Prompt**: “Provide Swift code for a WKWebView iOS app loading KingSurf’s interface and fetching synced workspace definitions.”  
- [ ] 8.4 Testing Mobile Shells  
  - **Description**: Test on emulators/devices; verify navigation, workspace switching, summary fetch.  
  - **Dependencies**: 8.2 & 8.3 implemented.  
  - **Deliverables**: Test reports; issue list.  
  - **CI Adjustments**: Document manual build/test steps or integrate mobile CI if available.

---

## Stage 9: Post-Core Enhancements & Monitoring
*(Requires core features live in production)*

- [ ] 9.1 Telemetry for Feature Usage (opt-in)  
  - **Description**: Anonymized usage stats for feature adoption (workspaces, AI helpers).  
  - **Dependencies**: Core features released.  
  - **Deliverables**: Telemetry schema; implementation respecting privacy.  
  - **AI Prompt**: “Draft telemetry schema for anonymized feature usage in KingSurf with user consent.”  
- [ ] 9.2 Continuous Performance Monitoring  
  - **Description**: Automate performance checks on new builds; alert on regressions.  
  - **Dependencies**: CI benchmark jobs (Stage 4).  
  - **Deliverables**: CI alerts/dashboard integration.  
  - **AI Prompt**: “Generate CI job config to run performance benchmarks on each PR and flag regressions.”  
- [ ] 9.3 Advanced AI Workflows  
  - **Description**: Deeper automation routines combining multiple features (beyond initial automated workflows).  
  - **Dependencies**: 7.3 automated workflows; telemetry data.  
  - **Deliverables**: Workflow UI enhancements; orchestration engine.  
  - **AI Prompt**: “Design UI for users to chain multiple AI/browser actions (e.g., collect tab data, summarize, export) and execute them.”  
- [ ] 9.4 Built-In Messaging & Collaboration Extensions  
  - **Description**: Integrate with chat/community feeds for link/note sharing in-browser.  
  - **Dependencies**: 7.7 messaging panel scaffold; sync backend.  
  - **Deliverables**: Integration modules; UI components.  
  - **AI Prompt**: “Generate code stub for a messaging sidebar that integrates with a collaboration API to share links/notes.”  
- [ ] 9.5 Bookmark & History AI Insights  
  - **Description**: Refine bookmark grouping and history resurfacing using AI and telemetry.  
  - **Dependencies**: 7.6 bookmark insights scaffold; 9.1 telemetry.  
  - **Deliverables**: Analysis module; UI adjustments.  
  - **AI Prompt**: “Write pseudocode for analyzing telemetry-collected browsing data to recommend bookmark grouping and surface important pages.”  

---

## Success Criteria (Updated)
- **MVP Desktop Release**: Stable build with vertical tabs & theming, passes automated tests, distributed on Windows/macOS/Linux.  
- **Core Features Live**: Workspaces, AI helpers, privacy dashboard, tab sleeping, split view, timeline, focus mode, task list, permission guidance, phishing alerts, gesture/voice controls, theming & per-site styles—all implemented, tested, within performance targets.  
- **Sync & Mobile**: Encrypted sync working; Android/iOS shells load correct data, minimal UI for core tasks.  
- **User Feedback & Metrics**: Opt-in telemetry showing >50% workspace usage, >30% AI-helper usage; performance within targets.  
- **Quality & Stability**: No critical production bugs; CI enforces tests; memory/regression checks automated.  
- **Adoption & Satisfaction**: Growing downloads; positive user feedback; high ratings.

---

*All completed items remain marked [x]. New tasks are ordered so prerequisites appear before dependents. This ensures implementation follows the correct sequence of infrastructure → UI foundation → feature layers → integration → monitoring.*
