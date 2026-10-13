# TDD verification reporting

Use this shared reporting policy for standalone TDD and every adapter. Deliver results in chat; no separate report file is required. Keep the report proportional to the change.

For each tested behavior or coherent group, include:

- Behavior verified and linked acceptance-criterion IDs when available.
- Public test boundary and test-file pointers. Use repository-native scope labels, but explain which real collaborators ran and which boundaries were mocked or faked.
- Focused and relevant broader commands with actual outcomes: passed, failed, not run, or not applicable. Disclose unrelated pre-existing failures separately from task regressions.
- Coverage limits and uncovered requirements, including runtime, browser, persistence, or external integration behavior the chosen tests cannot establish.

Passing a package/service, DOM, direct-export, or domain test is evidence only for what that test exercised. Distinguish missing behavior from missing verification. Do not mark an unrun check as passed or imply a fake proves the real integration.

When coordinated by `implement`, supply this evidence to its consolidated phase or delivery report without a duplicate adapter report. The coordinator owns audit, CodeRabbit, plan status, and final manual QA. Standalone TDD reports its tests and limitations without starting that delivery workflow.
