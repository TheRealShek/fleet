# Validate the voice skill

Use this guide only when testing or maintaining the skill. Ordinary drafting needs the voice profile, not the evaluation material.

Use the requests in [cases.json](cases.json) to test actual writing. Select cases affected by a change and add unfamiliar holdouts before declaring the change complete. Do not show the writer an expected answer or an evaluator's suspected defect before the first attempt. Use another agent only when the user has authorized delegation, and respect any limit on the number of agents.

Keep generated drafts and execution logs in a temporary directory outside the repository. Do not save generated answers as voice references. Read the installed entrypoint and complete profile, then produce the requested drafts without changing the requests.

Inspect the output independently of the writer's self-assessment. Check:

- Supplied facts, measurements, narrator, units, uncertainty, exact quotations, and identifiers survive.
- Word limits and explicit formats are met, or an unavoidable conflict is reported honestly. Never count a shorter output as a length pass. Fuller input is a separate test, not a retroactive pass for sparse input.
- The opening, prerequisite detour, mechanism, example, and return to the original question fit the content. Compare the pattern against the source analysis rather than counting catchphrases.
- Research prose makes a supported local judgment and explains the mechanism. It does not repeat a generic caution template in place of an argument.
- Personal prose adds no invented biography, advice, or filler recap. Procedures address their readers rather than explaining the drafting prompt.
- Explicit spelling and format requests take precedence over defaults. Exact quotations and identifiers survive even when they contain otherwise discouraged wording or punctuation.

Fix only concrete findings supported by the drafts or sources. Recheck affected cases, then run another holdout batch. Stop after two successive batches reveal no new actionable findings and structural checks pass. Do not keep adding prohibitions to polish already acceptable prose.

Record both passes and limitations. Distinguish readable installation links, provider catalog discovery, actual skill use, and subjective voice fidelity. One does not prove the others. The initial run is recorded in [validation.md](validation.md).
