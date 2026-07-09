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

## Usage

Once installed, just talk to your agent naturally. Each skill triggers automatically based on what you ask for — no extra configuration needed.

## License

MIT
