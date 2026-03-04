# Gong Account Research Skill

A Claude Code skill that enables AI-powered research of customer accounts using their complete Gong call transcript history.

## What it does

This skill allows Claude to automatically fetch and analyze all recorded calls for a specific account, providing instant answers about:

- **Pain points** - What challenges and frustrations the customer mentioned
- **Tech stack** - Technologies, tools, and platforms they use or discussed
- **Key contacts** - Who's involved, their roles, and level of engagement
- **Deal status** - Current state of opportunities, blockers, and objections
- **Competitor mentions** - Which vendors they're evaluating or comparing
- **Recent discussions** - What was covered in the latest calls

## Prerequisites

1. **Python 3** installed on your system
2. **Gong API access** with proper credentials configured
3. **Gong API script** at `/Users/vishwasrinivasan/claude-work/gong_account_transcripts.py`
4. **Claude Code** installed and running

## Installation

### Personal Installation (Available in all projects)

```bash
# Clone this repository to your Claude skills directory
cd ~/.claude/skills
git clone https://github.com/imnotcarlosboozer/gong-transcript-skill.git gong-account-research
```

### Project-Specific Installation

```bash
# Clone to your project's .claude/skills directory
cd /path/to/your/project
mkdir -p .claude/skills
cd .claude/skills
git clone https://github.com/imnotcarlosboozer/gong-transcript-skill.git gong-account-research
```

## Usage

### Direct Invocation

Invoke the skill directly with an account name:

```
/gong-account-research Iron Mountain
```

With a specific question:

```
/gong-account-research Iron Mountain - what are their pain points?
```

### Automatic Invocation

Claude will automatically load this skill when you ask relevant questions:

```
What pain points has Iron Mountain mentioned?
What's the tech stack at Acme Corp?
Who's the main contact at Global Solutions?
What's blocking the deal with Enterprise Inc?
```

### Follow-up Questions

After the initial research, ask follow-up questions and Claude will use the already-loaded transcripts:

```
Are they evaluating any competitors?
What did we discuss in the last call?
What objections have they raised?
```

## Features

- **CRM-Matched Search** - Automatically matches calls by Salesforce account name
- **Full Transcript Access** - Every word from every call is available for analysis
- **Structured Output** - Saves data in both JSON (raw) and Markdown (readable) formats
- **Smart Pagination** - Handles large accounts with many calls automatically
- **Context-Rich** - Includes CRM metadata like ARR, opportunities, and health notes
- **Speaker Attribution** - Identifies who said what in each call

## How it Works

1. **Fetches Transcripts** - Runs a Python script that queries the Gong API with extended context
2. **Saves Data** - Stores transcripts in both JSON and Markdown formats
3. **Analyzes Content** - Claude reads and analyzes the full transcript history
4. **Answers Questions** - Provides specific, quote-backed answers to your questions

## Output Files

The skill generates files in `/Users/vishwasrinivasan/claude-work/`:

- `gong_[account]_[date].json` - Raw API response data
- `gong_[account]_[date].md` - Formatted transcripts with speaker names

## Examples

### Research pain points
```
/gong-account-research Salesforce - what are their main pain points?
```

### Identify decision makers
```
/gong-account-research Microsoft - who are the key contacts?
```

### Understand tech stack
```
What technologies does Amazon mention in their calls?
```

### Check deal status
```
What's blocking the deal with Google?
```

### General overview
```
/gong-account-research Apple
```

## Configuration

The skill uses these default settings:

- **Time range**: 12 months of call history
- **Format**: Both JSON and Markdown outputs
- **Context**: Extended (includes CRM associations)

To customize, modify the Python script parameters in `SKILL.md`.

## Troubleshooting

### "Account not found"
Try listing available accounts first:
```bash
python3 ~/claude-work/gong_account_transcripts.py "" --list-accounts --months 3
```

### Large transcript files
For accounts with 50+ calls, Claude will automatically read the markdown file in chunks.

### API rate limits
The script includes automatic rate limiting and retry logic.

## Contributing

Contributions welcome! Please submit issues or pull requests on GitHub.

## License

MIT License - feel free to use and modify as needed.

## Related Resources

- [Claude Code Documentation](https://code.claude.com/docs)
- [Agent Skills Standard](https://agentskills.io)
- [Gong API Documentation](https://help.gong.io/hc/en-us/sections/360007831554-API-Documentation)
