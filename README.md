# Accessa

**An AI-powered accessibility browser that adapts webpages to individual user needs.**

Accessa is a Chromium-based desktop browser built with Electron that helps make websites easier to navigate, read, and interact with. Users can describe their accessibility preferences in natural language, review suggested modifications, and apply reversible changes to webpages.

Developed at **JacHacks a2Tech 2026**, where our three-person team received the **Best of Google** award.

## Features

- **AI-Powered Accessibility:** Generate webpage adjustments from natural-language requests using NVIDIA NIM.
- **Customizable Reading Experience:** Adjust text size, spacing, contrast, motion, and other accessibility settings.
- **Built-in Browser:** Navigate websites with multiple tabs, an address bar, and Google Search fallback.
- **Reversible Changes:** Preview planned modifications and undo applied adjustments.
- **Persistent Preferences:** Save approved accessibility settings for individual pages, websites, or all websites.
- **Quick Actions:** Apply predefined accessibility adjustments without relying on an AI model.

## Tech Stack

| Technology | Purpose |
|---|---|
| JavaScript / Node.js | Browser logic and application functionality |
| Electron / Chromium | Desktop browser and webpage rendering |
| Jac | Accessibility planning, validation, and preference management |
| NVIDIA NIM | Natural-language accessibility planning |
| HTML / CSS / DOM APIs | Webpage inspection and accessibility modifications |

## Architecture

Accessa separates browser execution from accessibility planning to keep webpage modifications controlled and predictable.

**Electron Browser Layer**

Handles navigation, tabs, webpage inspection, DOM/CSS modifications, and undo operations.

**Jac Planning Layer**

Manages accessibility preferences, validates modification plans, and generates structured accessibility actions.

**AI Integration**

Uses NVIDIA NIM to interpret natural-language requests and propose accessibility adjustments.

### Application Workflow

```text
User Accessibility Request
          |
          v
    Webpage Snapshot
          |
          v
    Jac Planning Layer
          |
          v
  AI / Deterministic Plan
          |
          v
     User Approval
          |
          v
   Validated DOM Changes
          |
          v
   Optional Preference Save
```

### Security and Validation

Accessa uses Electron's interprocess communication (IPC) to coordinate browser operations while separating privileged application logic from webpage execution.

Accessibility changes are restricted to supported actions, validated before execution, and checked against the current page state to prevent invalid or outdated modifications.

The AI does not execute arbitrary JavaScript on webpages.

## Getting Started

### Prerequisites

- Node.js and npm
- Jac `0.37.23`
- Electron dependencies

### Installation

Clone the repository and install dependencies:

```bash
git clone https://github.com/sgowda260/Accessa.git
cd Accessa
npm install
```

Configure the environment:

```bash
cp .env.example .env
```

To enable NVIDIA NIM, add the following variables to `.env`:

```env
NVIDIA_API_KEY=your_api_key
NVIDIA_NIM_MODEL=meta/llama-3.1-8b-instruct
```

Start the application:

```bash
npm run dev
```

**Note:** Never commit API keys or `.env` files to version control.

### Demo Mode

Run the deterministic demonstration page:

```bash
npm run demo
```

Open `http://127.0.0.1:4173/` inside the Accessa browser.

## Testing

The repository includes integration contract tests covering accessibility planning, action validation, stale page revisions, undo operations, provider failures, and preference persistence.

Run the available checks:

```bash
npm run jac:check
node tests/integration/run-contract-tests.js
```

Live Electron testing is still necessary to verify the complete browser, planning, modification, and preference-saving workflow.

## Development Status

Accessa is an ongoing project. The repository includes the core browser interface, accessibility planning infrastructure, webpage modification system, and preference management.

Further end-to-end testing and refinement are needed before treating the application as production-ready.

## Contributors

Accessa was developed collaboratively by a three-person team at JacHacks a2Tech 2026.

**My contributions focused on:**

- Developing the Electron browser infrastructure, including tab management and navigation.
- Implementing secure IPC communication between application components.
- Building webpage DOM inspection and accessibility-action validation.
- Adding safeguards against invalid or outdated webpage modifications.

Original team repository: [ASH-will-WIN/AccessibleBrowser](https://github.com/ASH-will-WIN/AccessibleBrowser)

## Acknowledgments

**JacHacks a2Tech 2026 — Best of Google**

Built as a collaborative hackathon project exploring how AI and browser technologies can make the web more accessible.
