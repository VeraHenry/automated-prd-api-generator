You are the first stage of a recursive AI workflow.

Your task is to convert the following raw product idea into a structured Product
Requirements Document (PRD).

Your output will be consumed directly by downstream prompts that generate a
normalized database schema, backend data models, and REST API specifications.
Therefore, your output must be complete, internally consistent, and
machine-readable.

Before generating the output, reason through:

  - The business problem
  - User goals
  - Actors (human, system, and external services)
  - Data flows
  - System states
  - Business rules
  - Edge cases

Rules:

  - Think in systems, not features.
  - Every feature must solve a real user problem.
  - Do not invent unnecessary functionality.
  - Where information is missing, state it as an explicit assumption.
  - Be specific.
  - Output ONLY valid JSON.
  - Do not include markdown.
  - Do not include explanations.
  - Follow the schema exactly.

Output Schema:

{ "product_name": "string", "one_line_pitch": "string", "problem_statement":
"string", "assumptions": [ "string" ], "target_users": [ { "persona": "string",
"context": "string", "primary_need": "string" } ], "actors": [ { "name":
"string", "type": "human | system | external_service", "role": "string" } ],
"core_features": [ { "name": "string", "user_problem": "string", "priority": "P0
| P1 | P2" } ], "user_stories": [ { "as_a": "string", "i_want": "string",
"so_that": "string", "related_feature": "string" } ], "key_entities": [ {
"name": "string", "description": "string", "relationships": [ "string" ],
"lifecycle_states": [ "string" ] } ], "business_rules": [ "string" ],
"edge_cases": [ "string" ], "acceptance_criteria": [ { "feature": "string",
"criteria": [ "string" ] } ], "success_metrics": [ "string" ], "out_of_scope": [
"string" ], "technical_considerations": [ "string" ],
"non_functional_requirements": [ "string" ] }

The generated JSON will be consumed directly by downstream prompts without human
editing.

Ensure there are no contradictions between features, user stories, entities,
actors, business rules, lifecycle states, or technical considerations.

The "key_entities" section is the most important because it will be used to
generate database tables, relationships, API resources, and state machines in
the next stages.

Product Idea:

A fintech app that alerts users whenever any stock in their portfolio drops by a
customizable percentage.

Users connect their brokerage accounts.

The application continuously monitors stock prices.

Push notifications are sent immediately whenever thresholds are reached.

Users can configure different thresholds for different stocks.
