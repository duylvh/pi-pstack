# Review models in Pi

Read this before Arena, Interrogate, or Architect's Arena runners spawn a panel.
It covers how the `Agent` tool from `@tintinweb/pi-subagents` picks a model, and how to report what ran.

## Seats

The injected role table keeps one seat per array entry, in order.
`inherit-parent` and `auto` keep their seat but omit `model`, so that seat runs on the parent session model.
With no panel configured, Arena and Interrogate run two seats on the parent model.
Run `/pstack status` to see each seat's effective model, resolved against the current parent, and any configured selector this session cannot reach.

## How `Agent` resolves `model`

- Pass the exact `provider/id` from the role table.
- `Agent` matches an exact available `provider/id` first. When it finds none, it fuzzy-matches the string against available models, then retries the bare id under any provider. A typo or a stale selector can therefore run on a different model instead of failing. It returns an error only when nothing matches.
- An agent file's own `model` or `thinking` overrides the value you pass. `poteto-agent` and `general-purpose` set neither, so your values apply.
- Set reasoning with the `thinking` input (`off`, `minimal`, `low`, `medium`, `high`, `xhigh`, or `max`). Never append a level to `model`, such as `provider/id:high`: `Agent` would fuzzy-match that string to some model rather than read it as a level. Pi clamps a level the model does not support.

## Report what ran

Report the model each seat actually ran on, from its `Agent` result or `get_subagent_result`, not the selector you asked for.
Call a panel whose seats ran on one model a same-model panel, not multi-model or cross-family review.
Different selectors do not prove different model families, and different `thinking` levels on one model add no model diversity.
A missing reviewer is not a completed reviewer.

## Failures and fallbacks

When a seat's selector is rejected or unavailable, name the seat and the error, keep the results that finished, and do not send that selector again in this run.
Where the skill allows a fallback, rerun that seat with `model` omitted and say the panel lost diversity.
Keep the requested seat count through fallbacks, or name each missing seat.
If the user required a specific model or model diversity, report that seat blocked instead of substituting another model.
Do not pick another paid provider, or add seats, only to raise diversity. Offer `/setup-pstack` for an opt-in panel of confirmed available models instead.

## Arena cross-judge

The cross-judge pool lists choices for one judge, not extra seats.
Try only available entries from a model family other than the parent's, in pool order.
`inherit-parent` and `auto` never judge.
If no eligible entry runs, or you cannot tell the parent's family, skip the judge and say why. You still score every candidate and pick the base in Phase D.
The default pool is all `inherit-parent`, so there is no cross-family judge until the user configures one.
