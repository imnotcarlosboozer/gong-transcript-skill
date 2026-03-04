---
name: gong-account-research
description: Research accounts using their complete Gong call transcript history. Use when users ask about account pain points, tech stack, contacts, or deal status.
allowed-tools: Bash(python3 *), Read
---

# Gong Account Research

Answer questions about an account using their complete Gong call transcript history.

## Input
The user has provided: $ARGUMENTS

This could be:
- An account name with a question: "Iron Mountain - what are their pain points?"
- Just an account name: "Iron Mountain" (give a general overview)
- A follow-up question about a previously loaded account

## Steps

### 1. Fetch Transcripts

Run the script to pull all calls and transcripts for the account:

```bash
python3 /Users/vishwasrinivasan/claude-work/gong_account_transcripts.py "ACCOUNT_NAME" --months 12 --format both
```

This uses the Gong API with `context: Extended` to match calls by their **CRM Account Name** (Salesforce association), pulls full transcripts, and saves:
- `/Users/vishwasrinivasan/claude-work/gong_[account]_[date].json` — raw data
- `/Users/vishwasrinivasan/claude-work/gong_[account]_[date].md` — readable transcripts

If unsure of the exact account name, list available accounts first:
```bash
python3 /Users/vishwasrinivasan/claude-work/gong_account_transcripts.py "" --list-accounts --months 3
```

### 2. Read and Answer

Read the generated markdown file. If it's large, read in chunks.

Use the full transcript history to answer whatever the user asked. You have every word said on every call — use it.

If no specific question was asked, provide a brief overview:
- What recent calls covered
- Key contacts and their roles
- Current state of the relationship

### 3. Stay Ready for Follow-Ups

The user will likely ask follow-up questions. You have the transcripts loaded, so answer directly:
- "What's their tech stack?" — search transcripts for technology mentions
- "What pain points did they mention?" — find complaints, frustrations, challenges
- "Who's the main contact?" — look at who appears most and speaks most
- "What did we discuss last call?" — read the most recent transcript
- "Are they evaluating competitors?" — find any vendor/competitor mentions
- "What's blocking the deal?" — find objections, concerns, timing issues
- Anything else — just search the transcripts

## Notes
- The script handles pagination, rate limiting, and CRM matching automatically
- Transcripts include speaker names, so you can attribute quotes to specific people
- CRM context (ARR, opportunities, health notes) is included in the output
- For very large accounts (50+ calls), the markdown file may need to be read in sections
