# Rule 7: Use AI within explicit task boundaries

The table below maps each rule to appropriate AI use cases and the human check each requires. It serves as a reference for deciding whether a given task falls within the scope of reliable AI assistance.

| Rule | Possible use cases | Required human check |
|---|---|---|
| Rule 1: Project structure | Inspect a folder tree and suggest missing folders, README sections, or organization issues. | Confirm that suggested paths match the actual repository and lab conventions. |
| Rule 2: Version control | Draft commit messages or summarize a change. | Inspect the diff before committing. |
| Rule 3: Documentation | Draft README sections, summarize scripts, or turn meeting notes into a decision log. | Check that commands, paths, assumptions, and decisions are accurate. |
| Rule 4: Reusable code | Refactor duplicated code into functions or identify repeated code blocks. | Run old and new code on a small example and compare outputs. |
| Rule 5: Environment | Identify missing dependency files or explain environment setup commands. | Recreate the environment from the recorded files. |
| Rule 6: Automation | Draft wrapper scripts, workflow definitions, or logging checks. | Run the workflow on test inputs and inspect logs and outputs. |
| Rule 8: Names and metadata | Compare column names, event labels, or task variables against a data dictionary. | Confirm mappings against task logic and source files. |
| Rule 9: Analytic inputs and outputs | Draft QC templates, exclusion tables, or report summaries. | Verify counts, exclusions, and flags against actual outputs. |
| Rule 10: Lab defaults | Draft onboarding material or check whether a project follows lab conventions. | Have a human analyst test the instructions. |

## What to provide to the AI?

For most coding tasks, the AI needs documents and metadata sufficient to infer the structure of the analysis, not the data itself. Code files, folder structure, data dictionaries, schemas, and documentation can generally be shared. Participant data should not be shared with external AI tools unless explicitly permitted by institutional policy, and the tool is approved for that use; in most cases, a data dictionary and a small synthetic or anonymized example are sufficient for the AI to generate and test code. Agentic tools that require broader repository access should be run on a repository in which participant data are stored separately, following the structure introduced in Rule 1.

## Prompting AI tools for specific, bounded tasks

AI tools used for project work fall into two categories depending on how they access files. Agentic tools and IDE assistants — such as Claude Code, GitHub Copilot, or Cursor — can read the project directory directly and do not need file contents pasted into the prompt. Chat interfaces cannot access the repository and require the analyst to paste the relevant files into the conversation. The prompt structure described here applies to both; the difference is that with a chat interface, the files listed under "files to read" need to be included in full.

In both cases, the AI should always be required to write out its plan before changing anything. An AI that has misunderstood the task will reveal that misunderstanding in the plan, where it costs nothing to correct. After the task, the AI should also produce a brief report of what it actually did, which becomes part of the provenance record for that change.

The prompt has three parts: the task description, a standard instruction block that stays the same across every prompt, and a report request. Only the task description changes.

```text
Task: [one sentence]
Target: [file, function, or line range]
Files to read: [files the AI should consult]
Files you may modify: [explicit list]
Files you must not modify: [explicit list]
Success looks like: [one sentence describing correct output]
Scope boundary: [what this task explicitly does not include]

Before making any changes, write out:
- which files you will read
- which files you will modify and how
- which files you will not touch
- any assumption not stated in the task above

Do not proceed until the analyst has confirmed the plan.

Once the task is complete, write a short report stating:
- which files were changed and what changed in each
- any assumption you made that was not explicit in the task
- any decision you encountered that fell outside the constraints,
  and how you handled it or why you stopped

If at any point the task requires a decision not covered by
the constraints above, stop and describe the situation
rather than proceeding.
```

The workflow that follows has three steps. First, read the plan the AI produces and confirm it matches what was intended before authorizing execution. Second, review the changes the AI made before committing them to version control. Third, for coding requests specifically, and before committing, confirm that the code runs cleanly from a fresh session, passes a small test case with known output, and introduces no new dependencies that are not already recorded in the environment specification. The AI report then accompanies the commit as the provenance record for that change.

Labs that want a formal governance structure for multi-step agentic tasks — covering role separation, audit trails, and workflow-level handoffs — can find an implementation at <https://github.com/ValentinGuigon/SUPLEX-agentic-workflow>.
