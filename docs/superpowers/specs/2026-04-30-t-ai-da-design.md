# T-AI-DA Design

## Purpose

Prepare the document package for the AWS Summit Japan 2026 AI-DLC Hackathon
document screening. The submission will be a public GitHub repository containing
README and AI-DLC Inception phase artifacts.

## Product Concept

T-AI-DA is an AWS-based decision delegation service for single-person
businesspeople who are tired of making everyday life decisions.

The name combines "Taida" (laziness) and "AI". The concept is to thoroughly
spoil the user by removing small daily decisions. The service starts with a
morning "today's life plan" and supports an on-demand instant decision button.

The final vision is an "life OS" that delegates decisions across daily life,
consumption, lifestyle, health-related routines, and relationships, while the
MVP focuses on low-risk daily decisions.

## Target User

The primary persona is a single-person business professional who has used most
of their cognitive energy at work and does not want to decide what to eat, wear,
buy, or do after work.

## Core Experience

T-AI-DA provides two main MVP experiences:

1. Morning life plan generation
   - Decides meals, clothes, movement, shopping preparation, and evening plans.
   - Presents a single recommended plan instead of a comparison-heavy list.

2. Instant decision button
   - Handles small questions such as what to eat, whether to buy something, or
     how to spend spare time.
   - Returns one decision with a short reason and preparation steps.

The product personality is an overprotective but slightly sarcastic butler. It
comforts the user while quietly weakening their decision-making muscles.

## Laziness Level Model

The service uses a progressive delegation model.

1. Suggestion mode
   - T-AI-DA proposes decisions and the user chooses.

2. Semi-automatic mode
   - T-AI-DA decides by default, but the user can reject or revise.

3. Automatic low-risk mode
   - For safe daily domains, T-AI-DA makes the decision and prepares the next
     action.

This progression is represented as a "laziness level". It turns the hackathon
theme into a product mechanic: the more useful T-AI-DA becomes, the less the
user has to decide.

## Scope And Guardrails

MVP scope:

- Meals
- Clothes
- Daily schedule suggestions
- Shopping candidates
- Weekend or evening plans
- Preparation support such as shopping lists, store candidates, routes, and
  order links

Future scope:

- Purchase history
- Calendar and health logs
- Lifestyle optimization
- Relationship-related suggestions with strict limits

Out of scope or approval-required decisions:

- High-value purchases
- Medical diagnosis or treatment decisions
- Legal, contract, employment, resignation, and breakup decisions
- Any decision with serious financial, health, legal, or relationship impact

## Submission Package

The repository will use two layers:

1. README for judges
   - Product one-liner
   - Target user and pain
   - Business intent
   - Theme fit
   - MVP experience
   - AWS architecture summary
   - Links to AI-DLC artifacts

2. AI-DLC artifacts under `aidlc-docs/`
   - `aidlc-docs/aidlc-state.md`
   - `aidlc-docs/audit.md`
   - `aidlc-docs/inception/requirements/requirements.md`
   - `aidlc-docs/inception/requirements/requirement-verification-questions.md`
   - `aidlc-docs/inception/user-stories/personas.md`
   - `aidlc-docs/inception/user-stories/stories.md`
   - `aidlc-docs/inception/plans/execution-plan.md`
   - `aidlc-docs/inception/application-design/application-design.md`
   - `aidlc-docs/inception/application-design/components.md`
   - `aidlc-docs/inception/application-design/component-methods.md`
   - `aidlc-docs/inception/application-design/services.md`
   - `aidlc-docs/inception/application-design/component-dependency.md`
   - `aidlc-docs/inception/application-design/unit-of-work.md`
   - `aidlc-docs/inception/application-design/unit-of-work-dependency.md`
   - `aidlc-docs/inception/application-design/unit-of-work-story-map.md`

## Initial Unit Breakdown

1. Decision Orchestrator
   - Builds the morning life plan and instant decisions.

2. User Context
   - Manages MVP context such as weather, schedule, preferences, location, and
     budget.

3. T-AI-DA Persona
   - Generates the overprotective but slightly sarcastic butler experience.

4. Laziness Level
   - Controls the transition from suggestion to semi-automatic and low-risk
     automatic decisions.

5. Safety Guardrails
   - Detects high-risk decision domains and forces approval or rejection.

6. Preparation Assistant
   - Produces shopping lists, store candidates, routes, and order links.

## Judging Strategy

The document package will intentionally map to the document-screening criteria:

- Business intent clarity
  - Show decision fatigue as the core pain and T-AI-DA as a deliberate decision
    delegation system.

- Unit decomposition appropriateness
  - Make the units explicit and connect each unit to stories and responsibilities.

- Creativity and theme fit
  - Present "laziness level" as the central product mechanic.

- Document quality
  - Keep the README easy to scan and the AI-DLC artifacts traceable, consistent,
    and structured.

## Approval Status

The user approved:

- Product direction: "laziness level increases" decision OS
- Name: T-AI-DA
- MVP scope: morning life plan plus instant decision button
- Target user: single-person decision-fatigued business professional
- Guardrail strategy: low-risk MVP, constrained future expansion
- Submission package structure
