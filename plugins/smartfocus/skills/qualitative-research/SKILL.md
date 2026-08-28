---
name: SmartFocus Qualitative Research
description: Auto-activates when the user discusses user research, feedback gathering, concept testing, usability testing, or wants qualitative insights on a design, feature, or product.
version: 1.2.0
---

# SmartFocus Qualitative Research

SmartFocus runs AI-powered focus groups with synthetic participants matching a defined
participant profile. Use it when the user needs qualitative directional feedback on a
design, feature, concept, or message.

## When to activate

- The user asks for user feedback, user testing, or a focus group.
- The user wants to understand how a target audience may react.
- The user wants to validate a product or design assumption.
- The user has a prototype, mockup, or draft copy and wants reactions.
- The user needs to compare design or message options.

## Honest framing — non-negotiable

Participants are simulated. Present findings as *directional qualitative signal from
synthetic participants*, never as evidence about real customers, quantitative market
sizing, or a substitute for talking to actual users on high-stakes decisions. When the
user will pass findings onward (to a client, a deck, an exec), remind them once to
label the methodology; how they frame it is their call.

## The intake determines the output

The single biggest quality lever is what you put into `run_focus_group`. Before calling:

1. **Pin the decision.** Ask what decision this research informs if it isn't obvious.
   Put it in `context` — FocusFox designs better sessions when it knows what hangs on
   the answer.
2. **Make the participant profile concrete.** "Users" produces mush. Occupations,
   behaviors ("canceled a meal-kit subscription in the last 6 months"), attitudes
   (mix skeptics with enthusiasts), and explicit exclusions produce sharp panels.
3. **State the market.** Include the country or region in the profile ("Belgian agency
   teams", "US community-bank customers"). SmartFocus localizes panels properly —
   names, employers, idiom — but only when it knows the market; don't make it guess.
4. **Pass stimuli when reactions matter.** A publicly reachable URL or image of the
   thing being judged beats a description of it.
5. **Let FocusFox author the questions** unless the user supplies a script they need
   asked verbatim — then pass their wording exactly in `questions` and say in
   `context` that the wording is fixed.

Prefer five participants for most product feedback; go smaller for fast exploration,
larger (up to 12) only when the user explicitly wants broader directional coverage.

## Workflow

1. Clarify the decision, then build the intake per the rules above.
2. Call `run_focus_group`. Tell the user it typically takes 5–10 minutes.
3. Poll `get_status` about every 30 seconds while the user wants to wait.
4. When complete, call `get_results` **with `includeTranscript: false`** — the shaped
   report (summary, key findings with quotes, recommendations) answers most questions
   at a fraction of the size. Fetch the full transcript in a second call only when you
   need to quote extensively, audit a specific exchange, or the user asks for verbatims.
5. Summarize for the user: the decision the research informed, what the panel
   converged on, where they split, and the recommended next move. Lead with what
   changed or was confirmed, not with a section-by-section recap.
6. Offer `follow_up` when there is an iteration to test: a panel matched to the prior
   session's composition receives the
   prior transcript and report as context, so it is the right tool for "we changed X
   based on your feedback — react to the new version," and the wrong tool for an
   unrelated topic (run a fresh group instead).

## Errors you should handle, not surface raw

- **`billing_limit_reached`** — the account has no plan or remaining group credit.
  Tell the user plainly: a paid plan or one-time project is needed before running a
  group, with the upgrade link from the error. Do not retry; nothing was created.
- **`Session not found`** — the sessionId is wrong or belongs to another account.
  Re-check the id from the original `run_focus_group` response before assuming failure.
- A run that stays in a non-completed status well past ~15 minutes is worth surfacing
  to the user rather than polling forever.

## Tool notes

- `generate_focus_group_plan` is **not implemented yet** — it returns a notice, not a
  plan. Never call it as a preview step; go straight to `run_focus_group`.
- Every completed run has a `viewUrl` — share it so the user can open the full session
  in SmartFocus itself.
