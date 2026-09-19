# DESIGN.md: Growth Indonesia Management App

## 1. App Context & Overview
**App Name:** Growth Indonesia
**Platform:** Android Native (Kotlin/Java/C)
**Domain:** Human Resources Development (Outbound, Training, Team Building, Traveling)
**Primary Goal:** A centralized management system for project creation, resource allocation, itinerary management, and offline-capable field execution.

## 2. Visual Language & Design System
Google Stitch must strictly follow **Material Design 3 (M3)** guidelines to ensure a native Android feel.

*   **Color Palette:**
    *   **Primary:** Forest Green (`#2E7D32`) - Represents growth, outdoor activities, and outbound nature.
    *   **Secondary:** Amber (`#FFC107`) - For warnings, pending actions, and highlights.
    *   **Surface/Background:** Off-White (`#F8F9FA`) - Clean layout for readability.
    *   **Text:** Dark Slate (`#1D1D1D`) for primary text, Gray (`#757575`) for secondary text.
*   **Typography:** Roboto or Sans-Serif equivalent. Use large, legible fonts for field use (accessibility).
*   **Component Style:** 
    *   Use Card-based layouts for projects and schedules.
    *   Floating Action Buttons (FAB) for primary actions (e.g., "Add Project", "Submit Report").
    *   Bottom Navigation Bar for core module switching.
    *   Visual indicators (badges) for `Offline Mode` status.

## 3. User Personas & Role-Based Access Control (RBAC)
The UI must adapt dynamically based on the active user role.

### A. Program Director
*   **Focus:** High-level management, project creation, and team monitoring.
*   **Key UI Elements:**
    *   Statistical Dashboard (Ongoing projects, available facilitators).
    *   Project Creation Wizard (Service Type selector: Outbound, Training, Team Building, Traveling).
    *   Rundown Builder interface.

### B. Trainer & Facilitator
*   **Focus:** Field execution, schedule checking, and reporting.
*   **Key UI Elements:**
    *   Schedule & ToR Viewer (Terms of Reference).
    *   Profile section displaying professional credentials (e.g., **HPOI Certification** badge).
    *   Prominent `Offline Mode` toggle/indicator for remote outbound areas (e.g., mountainous encampments).
    *   Field Reporting form with media upload capability.

### C. Admin & Logistics
*   **Focus:** Resource availability, ticketing, and equipment allocation.
*   **Key UI Elements:**
    *   Inventory Checklist.
    *   Participant Manifest table (for Traveling service).

## 4. Core User Flows (UI Navigation)

### Flow 1: Authentication & Role Routing
`Splash Screen` -> `Login Screen (Email/Password & SSO)` -> `Role Check`
*   If Program Director -> Redirect to `Director Dashboard`
*   If Facilitator -> Redirect to `Facilitator Dashboard`

### Flow 2: Project Management (Program Director)
`Director Dashboard` -> Click FAB (+) -> `Create Project Form`
*   **Step 1:** Details (Title, Client, Dates, Service Type Dropdown).
*   **Step 2:** Resource Allocation (Select Trainers/Facilitators).
*   **Step 3:** Rundown Builder (Timeline input).
-> Save to Cloudflare D1 (State: Draft/Ongoing).

### Flow 3: Field Execution (Facilitator)
`Facilitator Dashboard` -> `Upcoming Assignment Card` -> `Project Details`
*   **Tabs available:** Overview, Rundown, Team, Manifest.
*   **Action:** Toggle "Download for Offline Use" (Triggers local Room Database sync).
*   **Action:** Click "Submit Field Report" -> Opens reporting modal.

## 5. Google Stitch Specific Prompting Guidelines
When generating UI components from this DESIGN.md, Google Stitch should:
1.  **Prioritize Readability:** Facilitators will use this app outdoors. High contrast and large tap targets are mandatory.
2.  **State Management:** Always generate states for `Loading`, `Empty State` (e.g., "No upcoming assignments"), and `Offline/No Connection`.
3.  **Modular Components:** Generate the `Rundown Builder` as a drag-and-drop or sequential list UI component. Generate the `Participant Manifest` as a searchable data grid.
