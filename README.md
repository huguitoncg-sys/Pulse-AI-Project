# Finvisor: The Compliant Prospector 🏦🤖

Finvisor is a React-based, AI-powered CRM and prospecting tool designed specifically for financial advisors and wealth management professionals. It leverages the **Google Gemini API** to generate highly personalized outreach emails while enforcing strict FINRA/SEC compliance guardrails.

## ✨ Key Features

* **AI-Powered Email Generation:** Uses Gemini 2.5 Flash to automatically draft personalized outreach emails based on a prospect's role, recent liquidity events, and match reasons. Follows a strict "3-Sentence Framework" (Hook, Value, Guardrail).
* **Automated Compliance Engine:** Evaluates generated drafts against strict regulatory rules (e.g., no promised returns, no cherry-picked performance, mandatory FINRA/SIPC disclosures) before allowing the user to send.
* **Dual Operating Modes:**
    * *Autonomous Mode:* AI drafts the email, runs the compliance check, and automatically rewrites the draft if any compliance flags are triggered.
    * *Reviewer Mode:* AI generates a draft, allowing the advisor to manually edit the text before running a compliance check.
* **Intelligent Prospect Scoring:** Ranks prospects dynamically using a weighted composite score based on "ICP Match" (55%) and "Urgency Score" (45%).
* **Comprehensive Audit Trail:** Logs all generated emails, compliance pass/fail states, confidence scores, and timestamps. Includes a 1-click CSV export for regulatory record-keeping.
* **Keyboard-First Navigation:** Fully navigable via keyboard shortcuts for rapid, frictionless prospecting.
* **Custom Data Import:** Comes pre-loaded with top prospects, but supports custom `.json` file uploads for your own CRM data.

## 🛠 Tech Stack

* **Frontend:** React (Hooks: `useState`, `useEffect`, `useMemo`, `useCallback`)
* **Styling:** Native CSS-in-JS (Custom variables, responsive sidebar, CSS animations)
* **AI Integration:** Google Gemini API (`gemini-2.5-flash`) via REST fetch
* **Utilities:** Lodash (`_`) for data sorting and manipulation
* **Storage:** `localStorage` (for persisting the Audit Trail)

## 🚀 Getting Started

### Prerequisites
* Node.js (v16 or higher)
* npm or yarn
* A Google Gemini API Key

### Installation

1.  **Clone the repository and install dependencies:**
    (Assuming this is part of a standard React setup like Create React App or Vite)
    ```bash
    npm install
    # or
    yarn install
    ```

2.  **Add your Gemini API Key:**
    * *Important Security Note:* The provided `GeminiAPP.jsx` file contains a hardcoded API key (`const API_KEY = "..."`). **Do not commit your real API key to version control.**
    * For production, move this to an environment variable (e.g., `import.meta.env.VITE_GEMINI_API_KEY` or `process.env.REACT_APP_GEMINI_API_KEY`).

3.  **Run the development server:**
    ```bash
    npm start
    # or
    npm run dev
    ```

## ⌨️ Keyboard Shortcuts

Speed up your workflow using these built-in shortcuts:

| Key | Action |
| :--- | :--- |
| `↑` / `↓` | Navigate up and down the prospect list |
| `G` | Generate Draft / Run Auto-Draft (depending on current mode) |
| `C` | Run Compliance Check (when an email draft exists) |
| `Enter` | Approve & Log to Audit Trail (only works if compliance passes) |
| `Esc` | Deselect current prospect and return to list view |

## 📄 Custom Data Upload Format

You can upload your own prospects using the "LOAD DATA" button. The application expects a JSON array of objects with the following structure:

```json
[
  {
    "name": "Jane Doe",
    "current_role": "CEO at TechCorp",
    "location": "New York, NY",
    "linkedin_url": "[https://linkedin.com/in/janedoe](https://linkedin.com/in/janedoe)",
    "icp_match_score": 95,
    "urgency_score": 90,
    "matched_icp": "business_owners_exits",
    "summary": "Serial entrepreneur with recent exit.",
    "match_reasons": ["Recent $50M acquisition", "NYC based"],
    "why_now_reasons": ["Liquidity event last month creates tax needs"],
    "concerns": ["May already have advisory team"],
    "recommended_outreach_angle": "Congratulate on exit, offer tax-efficient structuring."
  }
]
