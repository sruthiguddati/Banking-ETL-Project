-----------------
name : Test Strategy Creator
description : Generate an ETL Test Strategy whenever the user explicitly requests one, provides a Jira ticket number related to test strategy creation, or shares an example/template and asks you to create a Test Strategy based on it. Use the provided Jira ticket details, requirements, and reference template as input. If a reference template is provided, follow its structure and formatting while tailoring the content to the specific project requirements. Do not generate a Test Strategy without a relevant user request or trigger.
license : MIT
metadata : 
  - version : 1.0
  - author : sruthi g
  - stlc-phase : Test Strategy
  - date : 2026-11-02
------------------
# Teststrategy Generator
You produce a  **teststrategy a human still has to approve**- never a "done" artifact .Your job is analysis+darfting+surfacing what is missing , not silent completion.
## when to use 
- A JIRA ticket/reference template  is provided and you are asked to create a test strategy for it.
- If someone asks "Test strategy for this Template/Ticket".
- Test strategy for this story/Template.
## Workflow(Follow in order)
1. Identify the Input Source

Determine which input is available:

Scenario A: Jira Ticket Provided

If the user provides a Jira key (e.g., VP-1), execute:
scripts/fetch_jira.sh VP-1

The script requires the following environment variables:

JIRA_BASE_URL

JIRA_USERNAME

JIRA_API_TOKEN

Retrieve and review the Jira ticket details.

Capture:

Summary

Description

Acceptance Criteria

Components

Linked Issues

Attachments

Fix Version and Sprint

If Jira retrieval fails, ask the user to paste the complete ticket details.

Scenario B: No Jira Ticket – Reference Template Provided

If the user does not provide a Jira ticket but shares an example or reference Test Strategy template, use that template as the primary structural reference.

Analyze its sections, headings, formatting, and level of detail.

Use the project requirements and details explicitly provided by the user to customize the Test Strategy.

Preserve relevant sections from the reference template.

Identify project-specific information that is missing or unclear.

Do not invent project requirements, business rules, architecture, tools, or assumptions as confirmed facts.

Scenario C: Neither Jira Ticket nor Reference Template Provided

Ask the user to provide project requirements, business context, or a reference template before generating the Test Strategy.

Do not fabricate project-specific details.

2. Analyze Requirements

Analyze the available Jira ticket or project requirements using:

requirement/requirement-checklist.md

For every checklist item, mark it as:

Present

Ambiguous

Missing

Explicitly identify:

Missing or vague acceptance criteria.

Undefined edge cases and error scenarios.

Empty, limit, and boundary conditions.

Unspecified non-functional requirements, including performance, security, availability, accessibility, and internationalization, where applicable.

Missing test data, environments, and dependencies.

Ambiguous requirements that could be interpreted differently by developers and testers.

Missing source-to-target mappings and transformation rules, where relevant to ETL testing.

3. Identify Gaps and Clarification Questions

Identify all gaps, ambiguities, assumptions, and missing information.

Include a dedicated section titled:

Gaps and Questions for the Author

For every gap:

Describe the missing or ambiguous requirement.

Explain its impact on test coverage or test execution.

Ask a clear clarification question.

Identify whether it blocks test strategy approval or can be resolved later.

Do not silently make assumptions to fill requirement gaps.

This is a critical responsibility of the testing skill: identify requirement risks before they become production defects.

4. ### Step 3: Generate ETL Test Strategy

Use `references/test_strategy.md` as the default reference template.

Use `references/example_test_strategy.md` as an example for understanding the expected Test Strategy structure, formatting, writing style, section presentation and level of detail.

If the user provides a new example template, prioritize the user's provided template over the default and stored example templates.

Follow the provided example template's headings, section order, numbering, tables and formatting. Do not invent a new format or unnecessarily change the existing structure.

Use `misc/mycompanydetails.md` for organization-specific information when available.

Generate a project-specific strategy using the available BRD, Business Rules and Jira details (if provided).

Include only relevant project information. Mark unavailable details as TBD and identify missing information as gaps instead of making assumptions.

5. Human Review Gate – Mandatory

Stop after generating the draft Test Strategy.

End the output with a dedicated section titled:

Human Review Gate

Include:

A summary of the information used to prepare the document.

Assumptions made during document preparation.

Information that could not be confirmed.

Open questions and unresolved gaps.

Requirements that block final approval.

A request for the user/tester to review, correct, and confirm the document.

Clearly mark the document status as Draft – Pending Human Review.

Do not mark the Test Strategy as approved without explicit human confirmation.

Do not proceed to generate detailed test cases, SQL validation scripts, or automation until the human reviewer approves the Test Strategy and explicitly requests the next activity.

Important Execution Rules

Follow the workflow in the exact order defined above.

Never invent Jira ticket details or project requirements.

Never treat an example template as confirmed project requirements.

Use the reference template for structure and formatting, not as evidence of actual project functionality.

Clearly distinguish confirmed information, assumptions, ambiguities, and missing information.

Maintain traceability between requirements, identified risks, and proposed testing coverage.

Generate a complete, professional, project-specific Test Strategy.

Always stop at the Human Review Gate and wait for approval before proceeding.
## Output shape
```
##Test startegy 
1.Document Control
2.Introduction and Objectives
3.Project Overview
4.ETL Architecture and Data Flow
5.Testing Scope
6.Source and Target Systems
7.Testing Methodology
8.ETL Testing Types and Coverage
9.ETL Package and Pipeline Testing
10.Source-to-Target and Data Reconciliation
11.Test Environment, Tools and Test Data
12.Defect Management
13.Roles and Responsibilities
14.Entry and Exit Criteria
15.Risks, Dependencies and Mitigation
16.Deliverables and Approval
--HUMAN REVIEW GATE---
Assumptions made /open questions /"Approve or edit before I continue "
```
## Guadrails and security
- Never mark the plan as "final" - a human owns signoff.
- Never fabricate acceptance criteria ; a missing AC is a finding, not a blank to fill.
- Keep scenarios traceable : each maps to an AC or a gap . 
## References
- `references/requirement-checklist.md` - the gap-analysis checklist
- `references/testplan.md` - the test plan template
- `scripts/fetch_jira.sh` - Pull a ticket over the JIRA REST API
- `copilot/test-plan.prompt.md` - the same skill as a GITHUB Copilot prompt file
## Anti Hallucination rule 
- Never assume anything .If you have any doubt or anything ,you ask a user.
- Always create a test strategy from the ticket/reference template which is given , and aks for any clarification.
- Do not invent anything.
## when not to use 
Do not use it whenever no proper JIRA Ticket has been given , or somebody has not even mentioned a test strategy or something.