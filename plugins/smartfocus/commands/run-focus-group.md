---
name: run-focus-group
description: Run an AI-powered focus group to get qualitative user feedback
---

Help the user run a SmartFocus focus group. Gather the following information conversationally, then call the `run_focus_group` MCP tool.

## Required information

1. What product, feature, design, or concept needs feedback?
2. What decision or research question should the focus group inform?
3. Who should participate, including relevant behaviors, context, and exclusions?

## Optional information

Ask only when it is not already clear from context:

1. Participant count. Default to five; the supported range is 3-12.
2. Specific questions that must be asked.
3. Discussion type, such as concept testing, usability testing, or brand perception.

## Execution

1. Call `run_focus_group` with the collected parameters. Include the market/country in
   the participant profile — SmartFocus localizes panels only when it knows the market.
2. Explain that the session is running and typically takes 5-10 minutes.
3. Poll `get_status` about every 30 seconds when the user wants to wait for it.
4. Call `get_results` with `includeTranscript: false` when complete and summarize
   decisions, risks, and recommended changes. Fetch the full transcript in a second
   call only when the user needs verbatims.
5. Use `follow_up` when the user wants the same panel to react to an iteration.

If the run is refused with `billing_limit_reached`, tell the user plainly that the
account needs a paid plan or one-time project and pass along the upgrade link — do not
retry, nothing was created. Do not call `generate_focus_group_plan`; it is not
implemented yet.
