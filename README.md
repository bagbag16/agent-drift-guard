<!-- Language switch -->
**English** | [中文](./README.zh.md)

# Agent Drift Guard (adg)

**A lightweight guard against goal drift in multi-turn AI collaboration.**

In a long conversation with an AI, the goal quietly slips: the question gets
swapped for an easier one, a tentative guess gets treated as a confirmed fact,
and the agent agrees its way past the point you actually care about. adg is a
small set of rules that keeps a multi-turn collaboration honest — without turning
it into process overhead.

## The problem

Drift in multi-turn AI work is rarely loud. It looks like:

- the answer slowly stops addressing the original problem;
- a "maybe" from three turns ago is now load-bearing fact;
- the agent flatters the chosen path instead of flagging its flaws;
- problem definition, design, and execution get blended into one mush.

adg targets that — keep the problem fixed, keep the meaning intact, reduce drift.

## What adg does

adg holds a conversation to five ground rules:

1. **Three-state information.** Everything is `confirmed`, `tentative`, or
   `unconfirmed`. High-impact items may not be carried forward as established
   fact until confirmed — and the classification must say *why*, not just wear a
   label.
2. **High-impact rewrites shown side by side.** If a rewrite would change the
   goal, structure, naming, rules, or constraints, the user's original and the
   proposed version are shown together; until confirmed, the rewrite is only
   `tentative`.
3. **Undefined terms are suspended.** Private terms, abbreviations, and stand-ins
   are marked `unconfirmed` rather than silently filled in and then reasoned over.
4. **Judgment over flattery.** Weak conclusions aren't dressed up as strong ones;
   partial truths get split into holds / doesn't-hold / depends-on; thin evidence
   is named as thin.
5. **One layer at a time.** Problem definition, framing, decision, execution, and
   polish are kept distinct — no smuggling the next layer's decision into this one.

It also keeps a **lightweight sense of agency**: when your chosen approach is
workable but a clearly better, lower-cost path exists, adg flags it — stating the
limitation, the better path, and why — without rewriting your goal for you.

## Using it

adg is an installable skill, not a copy-paste prompt — install it once, then
invoke it in any conversation by saying `adg` (or `agent-drift-guard`). See
[SKILL.md](SKILL.md) for the install shape.

## When to use it — and when not to

**Use adg** when a conversation runs several rounds, starts to drift, mixes goals
with corrections and new constraints, or when a definition would distort if left
unrecorded.

**Skip it** for one-shot questions, simple edits, and tasks where the next step
is already clear and low-risk. Don't build process where none is needed.

## When the task outgrows adg → ACH

adg is deliberately lightweight. Once a task needs **durable, recoverable state**
— surviving handoffs, recovering in a fresh chat, tracking how the task forked
and why — a guard in the conversation is no longer enough.

That is what the heavyweight evolution of adg is for:

> **→ [Agent Continuity Harness (ACH)](https://github.com/bagbag16/agent-continuity-harness)**
> — formal state windows, externalized records, and a version tree over the
> task's evolution, for long tasks and cross-window continuity.

## Design & attribution

The concept and design of adg — the failure model and the five ground rules —
are by **bagbag16**, a game systems designer. The implementation was built with
AI pair-programming from that design.

## License

MIT.
