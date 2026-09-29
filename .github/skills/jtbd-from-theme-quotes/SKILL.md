---
name: jtbd-from-theme-quotes
description: "Turn a theme group of stakeholder interview quotes into one evidence-grounded Jobs-to-be-Done (JTBD) statement. Use when selecting the strongest representative quote from a quote theme and writing the result to a new Markdown file."
argument-hint: "Provide a theme group, quotes, or a file containing them"
---

# JTBD From Theme Quotes

Create one traceable JTBD statement from one group of stakeholder quotes that share a theme.

## When to Use

- A stakeholder quote group or theme has already been selected.
- The user wants one JTBD statement grounded in the group's evidence.
- The result should be saved as a new Markdown file.

## Procedure

1. **Locate the evidence.** Use the quote group provided by the user. If they refer to a group in a workspace document, inspect that group and the original notes so each quote can be verified. Do not regroup unrelated quotes unless asked. If the intended group is ambiguous, ask which one to use.
2. **Identify the underlying job.** From the group's common theme, identify the person trying to make progress, the situation or trigger, the need or action, and the desired outcome. Treat tools and features as possible solutions, not as the job itself. Use only implications supported by the group's quotes.
3. **Select one representative quote.** Choose the single verbatim quote that most clearly and fairly encapsulates the job in the context of the theme. Prefer a quote that states the need, relevant situation, or intended outcome directly. Do not combine fragments from different quotes. Preserve its source ID and speaker details when available. If no single quote adequately represents the shared job, explain the mismatch and ask whether to narrow the theme or proceed with a qualified result.
4. **Write one JTBD statement.** Use this structure:
   - When [situation, context, or trigger],
   - I want to [underlying need or progress sought],
   - So that [desired outcome].

   Write from the perspective of the person doing the job, not automatically from the interviewee's perspective. Keep the statement solution-neutral and specific. Do not invent context, motivation, or outcomes. Identify the relevant stakeholder group in the output without adding separate assumption metadata.
5. **Create a new Markdown deliverable.** By default, save it as `submissions/jtbd-<theme-slug>.md`. Use a short lowercase hyphenated slug. Never overwrite an existing file; add a numeric suffix if the path already exists. If the user specifies another path, use that path.
6. **Review the result.** Confirm that the selected quote is exact and traceable, the statement is grounded in the theme, and the file contains exactly one selected quote and one JTBD statement. Use the theme as the section heading; do not add a separate theme explanation or quote rationale.

## Output Format

Use a concise structure like this:

```markdown
# Jobs to Be Done

## <Theme>

## Selected Quote

> "<Exact quote>"

**Source:** <Note ID; stakeholder name and role, when available>

### JTBD Statement

When <situation or trigger>, I want to <need or progress>, so that <desired outcome>.

**Stakeholder group:** <Relevant group, such as customers, collections representatives, or operations staff>
```

## Quality Checks

- The quote is copied exactly from the source and is the only quote selected as primary evidence.
- The statement captures an enduring need or progress, not a proposed feature or implementation.
- The situation, need, and outcome form a coherent statement and do not exceed what the evidence supports. The words "When," "I want to," and "so that" are not bolded.
- The relevant stakeholder group is named, without separate assumption metadata.
- The output is a new `.md` file and does not overwrite existing work.
