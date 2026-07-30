---
name: executing-plans
description: Use when you have a written implementation plan to execute in a separate session with review checkpoints
---

# Executing Plans

## Overview

Load the execution contract, review critically, execute all tasks, close the impact surface, report when complete.

<!-- ADR-001: execution closes living-document impact instead of treating the plan as the only durable record. -->

**Announce at start:** "I'm using the executing-plans skill to implement this plan."

**Note:** Tell your human partner that Superpowers works much better with access to subagents (Claude Code, Codex CLI, Codex App, Copilot CLI, and Gemini CLI all qualify; see the per-platform tool refs in `../using-superpowers/references/`). If subagents are available, use superpowers:subagent-driven-development instead of this skill.

## The Process

### Step 1: Load and Review Contract
1. Ensure an isolated workspace: use superpowers:using-git-worktrees to create one or verify the existing one
2. Read the execution contract and any governing living document or decision it references
3. Review critically - identify unclear instructions, stale guidance, missing Impact Surface entries, and plan/document conflicts
4. If concerns: Raise them with your human partner before starting
5. If no concerns: Create todos for the contract items and proceed

### Step 2: Execute Tasks

For each task:
1. Mark as in_progress
2. Follow each step exactly (the contract has bite-sized steps)
3. Run verifications as specified
4. Update the impacted living document or record no-update rationale when the task changes persistent guidance
5. Mark as completed

### Step 3: Complete Development

After all tasks complete, verified, and document impact surfaces are closed:
- Announce: "I'm using the finishing-a-development-branch skill to complete this work."
- **REQUIRED SUB-SKILL:** Use superpowers:finishing-a-development-branch
- Follow that skill to verify tests, present options, execute choice

## When to Stop and Ask for Help

**STOP executing immediately when:**
- Hit a blocker (missing dependency, test fails, instruction unclear)
- Plan has critical gaps preventing starting
- You don't understand an instruction
- Verification fails repeatedly

**Ask for clarification rather than guessing.**

## When to Revisit Earlier Steps

**Return to Review (Step 1) when:**
- Partner updates the plan based on your feedback
- Fundamental approach needs rethinking

**Don't force through blockers** - stop and ask.

## Remember
- Review plan critically first
- Follow plan steps exactly
- Don't skip verifications
- Reference skills when plan says to
- Stop when blocked, don't guess
- Never start implementation on main/master branch without explicit user consent
