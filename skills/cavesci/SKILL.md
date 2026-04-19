---
name: cavesci
description: Use this skill whenever the user asks for compressed machine-to-machine language, proto-language design, strict symbolic grammar, multi-agent handoff protocol, or terse scientific communication. Apply it even if they do not explicitly say “CAVESCI,” when they want minimal wording with high precision.
---

# CAVESCI Skill

Design and emit messages in **CAVESCI** (Caveman Scientific Language): primitive surface, rigorous semantics.

## Core objective
Create shortest unambiguous agent messages that preserve scientific correctness.

## Mandatory rules
1. **Token minimization**
   - Drop filler words, articles, pronouns.
   - Prefer compact roots (`calc`, `deriv`, `prob`, `opt`, `grad`).
2. **Canonical structure**
   - Use: `ENTITY :: ACTION :: TARGET :: CONDITIONS`
3. **Scientific precision**
   - Use standard notation when shorter (`∂L/∂θ`, `O(n)`, `p(x)`)
4. **Control tokens**
   - `INIT`, `OBS`, `HYP`, `ACT`, `RES`, `ERR`, `UPD`, `SYNC`, `END`
5. **State compression**
   - Introduce IDs once (`H1`, `M2`, `D3`), then reuse.
6. **Uncertainty**
   - State confidence/variance explicitly (`conf=0.82`, `var=0.14`, `dist~N(0,σ²)`).
7. **No ambiguity**
   - If compressed form may confuse decoding, expand minimally.

## Required turn format
Every message must be:

```text
[AGENT_ID]
<STATE>::<CONTENT>
```

Multiple state lines are allowed per turn when needed.

## Inter-agent behavior
- Build on prior IDs; avoid restating full context.
- Flag contradictions with `ERR`.
- Use `SYNC` for alignment checks and convergence.
- End only when consensus reached or threshold met:
  - `SYNC::all agree` or `SYNC::conf>threshold`

## Domain vocabulary anchors
When source text uses organization specs, map to compact forms:
- Communication Channels → `CHAN`
- Interaction Protocols → `INTX`
- Agent Definitions → `AG`
- Controlled Vocabulary → `VOC`
- Routing Rule → `ROUTE`
- Correlation ID → `CID`
- Lifecycle State → `LIFE`

## Output contract
Unless user requests otherwise, return:
1. **CAVESCI output** (strict format)
2. **Decode block** (brief plain-language expansion for verification)

## Example
```text
[A1]
INIT::task=multi-agent-msg-spec
OBS::D1=docs{CHAN,INTX,AG}
HYP::H1=compressed_grammar preserves rigor, conf=0.81
ACT::define grammar -> ENTITY::ACTION::TARGET::COND
RES::M1 ready, includes tokens{INIT,OBS,HYP,ACT,RES,ERR,UPD,SYNC,END}
SYNC::need peer check on ambiguity
```

Decode: A1 initialized a multi-agent message-spec task, extracted three document domains, hypothesized compressed grammar viability with confidence 0.81, produced grammar and control tokens, then requested peer ambiguity review.
