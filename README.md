# refocus-ai-insurance-tools

A collection of AI-powered tools for insurance agencies, brokers, and carriers — built and maintained by [ReFocus AI](https://www.refocusai.com).

These tools are free to use. They are designed for licensed insurance professionals working with AI assistants like Claude. Each tool reflects practices developed through real agency workflows.

---

## What is ReFocus AI?

ReFocus AI is an insurance technology platform that helps agencies and brokers retain clients, manage renewals, and automate remarketing. Learn more at [refocusai.com](https://www.refocusai.com).

---

## Tools

### Skills

These skills are structured instructions for AI assistants. Once added, they guide the assistant to analyze insurance documents using a professional framework. Install them from the Cursor or Claude desktop apps, Claude Projects, or other supported platforms below.

| Skill | Description |
|---|---|
| [Quote Comparison](./skills/quote-comparison/) | Compare two insurance quotes for the same insured side by side. Identifies premium differences, coverage gaps, rating discrepancies, and bind-readiness issues across any line of business. |

---

## How to Use a Skill

Each skill folder contains its own README with detailed usage
instructions and example prompts. Below are setup instructions
for the AI assistants that support custom instructions.

### Cursor & Claude (Desktop)

The Cursor and Claude desktop apps do not have a `/plugin`
command. Install skills from the UI instead:

1. Open **Settings** and go to **Customize**.
2. Under **Personal plugins**, click **+**.
3. Select **Create plugin and add marketplace**.
4. Click **Add from repository**.
5. Enter this repository URL:

   `https://github.com/refocus-ai/refocus-ai-insurance-tools`

6. Install the skills you want from the marketplace.
7. Open chat, upload your documents, and follow the prompts in
   that skill's README.

Skills load automatically when relevant. To invoke one manually,
see the skill's README for the correct command on your platform
(for example, `/skill-name` in Cursor or
`/plugin-name:skill-name` in Claude Desktop).

### Claude (claude.ai)

1. Open [Claude.ai](https://claude.ai) and create a new Project,
   or open an existing one.
2. Click **Project Instructions**.
3. Open the `SKILL.md` file in the skill folder (under
   `skills/<skill-name>/skills/<skill-id>/`), copy the full
   contents, and paste them into the Project Instructions field.
4. Save the instructions.
5. Upload your documents in the chat and use the example prompts
   from that skill's README.

### ChatGPT (chat.openai.com)

1. Open [ChatGPT](https://chat.openai.com) and go to
   **My GPTs** in the left sidebar.
2. Click **Create a GPT**.
3. Go to the **Configure** tab.
4. Copy the contents of the `SKILL.md` file from the skill folder
   and paste them into the **Instructions** field.
5. Save and open a conversation with your custom GPT.
6. Upload your documents and use the example prompts from that
   skill's README.

### Gemini (gemini.google.com)

1. Open [Gemini](https://gemini.google.com) and click **Gems**
   in the left sidebar.
2. Click **New Gem**.
3. Copy the contents of the `SKILL.md` file from the skill folder
   and paste them into the **Instructions** field.
4. Save the Gem and open a conversation with it.
5. Upload your documents and use the example prompts from that
   skill's README.

### OpenClaw (openclaw.ai)

OpenClaw uses a skills system that lets you extend your assistant
with custom behaviors. These skills are best suited for document
workflows you run frequently.

1. Install OpenClaw by following the
   [getting started guide](https://docs.openclaw.ai/getting-started).
2. Download the `SKILL.md` file from the skill folder in this repo.
3. In your OpenClaw chat interface, ask your assistant to load the
   skill file, or place it in your OpenClaw skills directory and
   ask your assistant to activate it.
4. Once active, upload your documents and use the example prompts
   from that skill's README.

For more detail on working with skills in OpenClaw, see the
[OpenClaw skills documentation](https://docs.openclaw.ai/skills)
or browse community skills on [ClawHub](https://clawhub.ai).

> **Note:** These skills are written and tested primarily for
> Claude. Results on other AI assistants may vary depending on
> how each platform interprets custom instructions.

---

## License

This repository is licensed under the [MIT License](./LICENSE). You are free to use, modify, and distribute these tools. Attribution to ReFocus AI is appreciated but not required.

---

## Contributing

We welcome contributions from the insurance and AI community.

### Reporting an Issue or Suggesting an Improvement

If you find a problem with an existing skill or have a suggestion
for improving it:

1. Go to the **Issues** tab at the top of this repository.
2. Click **New Issue**.
3. Describe the problem or suggestion clearly. Include the skill
   name, what you expected, and what you saw instead.
4. Submit the issue. We will review and respond.

### Adding a New Skill

If you have built a skill you would like to contribute:

1. Fork this repository.
2. Create a new folder under `skills/` named after your skill
   (e.g. `skills/policy-review/`).
3. Add a `SKILL.md` file with the skill content and a `README.md`
   with usage instructions following the same format as the
   existing skills.
4. Add `.cursor-plugin/plugin.json` and `.claude-plugin/plugin.json`
   manifests in the skill folder, and register the plugin in both
   `.cursor-plugin/marketplace.json` and `.claude-plugin/marketplace.json`
   at the repository root.
5. Open a Pull Request with a short description of what the skill
   does and who it is designed for.
6. We will review, test, and merge if it meets the quality bar.

---

## Contact

Questions or feedback? Reach out at [support@refocusai.com](mailto:support@refocusai.com) or open an issue in this repository.
