# Skills

A collection of AI agent skills, usable across Claude, Cursor, and other agent tools that support the skills format.

## Available skills

### Elite Adaptive Design Auditor

Audits UI/UX designs and frontend code, then gives professional-grade critique and improvement suggestions.

Triggers automatically when you:
- Upload an image of a UI/UX design (screenshot, mockup, Figma export, etc.)
- Share frontend code for a user interface
- Ask for a review, critique, or "pro" improvement of a layout
- Ask a specific question about one element (e.g. "is this color okay?") — the skill runs a full audit but prioritizes your specific question in the results

Example prompts:
- "Review this design"
- "What's wrong with this UI?"
- "How do I make this look more professional?"

### Elite Mobile Framework Auditor Ultimate

Audits mobile app projects (native and cross-platform), reviews architecture, performance, accessibility, security, and platform-specific best practices. It provides concrete remediation steps, code examples, and prioritised recommendations.

Triggers automatically when you:
- Share mobile app source code (Android, iOS, React Native, Flutter, etc.)
- Upload screenshots or recordings of mobile UIs
- Ask for a mobile-specific audit, performance tuning, or platform migration advice
- Ask a specific question about mobile behavior (e.g. "why is my app janky on Android?") — the skill runs a full audit but focuses on your question first

Example prompts:
- "Audit my Android app for performance"
- "How can I make this React Native app more battery efficient?"
- "Is this iOS architecture ready for scale?"

More skills will be added here over time.

## Installation

Install all skills:

```bash
npx skills@latest add kirubel12/skills
```

Install a specific skill:

```bash
npx skills@latest add kirubel12/skills/elite-adaptive-design-auditor
```

Install the mobile auditor skill:

```bash
npx skills@latest add kirubel12/skills/elite-mobile-framework-auditor-ultimate
```

## Usage

Once installed, just talk to your agent naturally. Each skill triggers automatically based on what you ask for — no extra configuration needed.

## License

MIT
