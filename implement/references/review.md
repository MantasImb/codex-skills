# CodeRabbit delivery review

Explicit use of `implement` includes the user's authorization to run `cr review --agent`, an authenticated third-party review that sends the repository context needed for review to CodeRabbit. Use the runtime's normal approval/escalation mechanism where required. This policy belongs here, not in TDD or its adapters.

After implementation, audit repairs, and passing relevant checks, run from the repository root:

```bash
cr review --agent
```

Run once for the full delivery, not once per phase. Establish what the actual review covered against the recorded task baseline, including relevant commits, working-tree changes, and new files. If its coverage differs, report the gap; never imply the complete task was externally reviewed without evidence. If additional CLI options are needed, inspect the installed help or current documentation rather than guessing syntax.

Read the complete output. Triage every finding as accepted, rejected, or already covered against requirements, repository guidance, and test evidence. Fix real in-scope correctness, regression, maintainability, and coverage problems. Explain rejected findings briefly, including false positives or conflicts with guidance. Capture actionable unrelated findings as deferred local issues. Unresolved findings blocking current requirements remain blockers.

After accepted fixes, rerun affected focused and broader checks and audit conclusions. After material review-driven changes, run one final `cr review --agent`; triage that output too. Address remaining real in-scope problems and disclose any changes made after the final review. Do not create an unbounded review loop.

If a genuine attempt is unavailable or cannot complete, skip this gate and continue delivery. Report the attempted command, observed failure and reason, and that external review is incomplete; never label it passed or substitute self-review for it. Do not infer rate limiting without evidence. This exception does not waive failing tests, audit defects, or other required checks. Preserve useful findings from partial output while stating that the review did not complete.

The user can request another review later in the same chat. Reuse current scope, rerun review on the current work, and apply the same bounded triage and verification policy. Do not schedule automatic retries.
