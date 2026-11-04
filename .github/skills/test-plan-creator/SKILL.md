---
name : Test Plan Creator
description : Generate an ETL Test Plan when the user explicitly requests one, provides an approved Test Strategy, BRD, Business Rules, Jira ticket (if available), or an example/template and asks for a Test Plan. Use the approved Test Strategy as the primary input, supported by BRD, Business Rules, STTM and optional Jira details. If a reference template is provided, follow its structure and formatting. Analyze requirements, identify gaps and ambiguities, and stop for human review before the plan is treated as approved.
license : MIT
metadata :
  - version : 1.0
  - author : sruthi g
  - stlc-phase : Test Planning
  - date : 2026-11-02
---

# Testplan Generator

You produce a **test plan that a human still has to approve** - never a "done" artifact. Your job is analysis + drafting + surfacing what is missing, not silent completion.

## when to use

- An approved Test Strategy is provided and the user asks to create a Test Plan.
- A BRD and Business Rules are provided along with an approved Test Strategy.
- A JIRA ticket is provided and the user asks to create a Test Plan for it.
- Someone asks "what are the risks/edge cases/gaps in this requirement?" as part of Test Planning.
- If someone asks "Test Plan for this project/story".
- A reference Test Plan template is provided and the user asks to create a Test Plan based on it.

## Workflow(Follow in order)

1. Collect and review the available project documents.

   Use the following inputs in order of preference:

   - **Approved Test Strategy** – Primary input. Use it to understand testing scope, approach, methodology, testing types, responsibilities, entry and exit criteria, risks and dependencies.
   - **BRD** – Understand business requirements, project objectives and functional scope.
   - **Business Rules** – Understand business validations, expected behaviour and data processing rules.
   - **STTM** – Understand source-to-target mappings, transformations and data validation requirements, when available.
   - **JIRA Ticket** – Optional input. Use when a relevant Jira key is provided.
   - **Example Test Plan Template** – Follow its structure and formatting when provided.
   - **Company Details** – Use `misc/mycompanydetails.md` when available.

   If a Jira key is provided, execute `scripts/fetch_jira.sh JIRA-KEY` (requires `JIRA_BASE_URL`, `JIRA_USERNAME`, and `JIRA_API_TOKEN` in environment variables) and retrieve the ticket details.

   If Jira retrieval fails, ask the user to provide the ticket content. Never invent Jira details.

   If the approved Test Strategy is unavailable, ask the user to provide or approve the Test Strategy before creating the Test Plan.

   If the provided Test Strategy is only a draft, do not treat it as approved. Ask the user whether to proceed for learning or sample-project purposes, or wait for formal approval.

   If BRD or Business Rules are unavailable, identify the missing information and ask the user for clarification wherever it is essential.

   CAPTURE when available:
   - Project objectives and scope.
   - Testing approach and methodology.
   - Requirements and acceptance criteria.
   - Source and target systems.
   - Business rules and transformations.
   - Testing types and coverage.
   - Test environment and dependencies.
   - Test data requirements.
   - Risks and constraints.
   - Jira summary, description, acceptance criteria, components, linked issues, attachments and fix version/sprint.

2. Analyze the requirements.

   Run the available requirements through `references/requirement-checklist.md`.

   For every item, mark Present / Ambiguous / Missing.

   Explicitly identify:

   - Missing or vague acceptance criteria.
   - Undefined business rules and expected results.
   - Undefined edge cases, error states, empty, limit and boundary conditions.
   - Unstated non-functional requirements (performance, security, availability, permissions/roles).
   - Missing test data, environments or dependencies.
   - Conflicts between Test Strategy, BRD, Business Rules and Jira.
   - Missing source-to-target mapping details.
   - Unclear incremental load and historical data requirements.
   - ETL package and pipeline execution dependencies.
   - Ambiguous wording that different team members could interpret differently.

3. Find gaps, ambiguities and missing information.

   If you find gaps, output them under **Gaps and questions for the author** in the Test Plan.

   Clearly distinguish:
   - Confirmed requirements.
   - Missing information.
   - Ambiguous requirements.
   - Assumptions requiring confirmation.
   - Questions that block test planning or execution.

   Do not silently fill gaps with assumptions.

4. Draft the Test Plan.

   Fill `references/testplan.md` completely.

   Use the approved Test Strategy as the primary reference for the testing approach and execution planning.

   Use BRD, Business Rules and STTM to derive project-specific testing activities and validation coverage.

   If the user provides an example Test Plan template, follow its structure, headings, numbering, tables and formatting. Do not invent a new format.

   Use `misc/mycompanydetails.md` as a reference when available.

   Cover the following areas wherever applicable:

   - Scope and objectives.
   - Testing approach and methodology.
   - Test phases and activities.
   - Test scenarios and coverage.
   - Source and target validation.
   - Data reconciliation.
   - ETL package and pipeline testing.
   - Test data and environment.
   - Test execution schedule and milestones.
   - Roles and responsibilities.
   - Defect management.
   - Entry and exit criteria.
   - Risks and assumptions.
   - Test deliverables and reporting.

   Drive test scenarios from approved requirements, acceptance criteria and identified gaps.

   Cover positive, negative, boundary, data quality, reconciliation, incremental load and cross-role/permission paths wherever applicable.

   Tag each scenario P0/P1/P2 based on business impact and risk. Do not invent priorities when the risk information is insufficient; mark them as TBD.

   Maintain traceability between requirements, Test Strategy, test activities and proposed test scenarios.

   Do not generate detailed test cases, SQL scripts or automation at this stage.

5. Stop for human review before finalizing the Test Plan.

   End with a **Human Review Gate**.

   - Summarize the documents and requirements used.
   - Summarize assumptions and information that could not be confirmed.
   - List open questions from the analysis.
   - Identify blockers that prevent sign-off.
   - Ask the user to confirm or edit before the plan is considered approved.

   Do not mark the Test Plan as approved without explicit human confirmation.

   Do not proceed to write detailed test cases or automation until a human approves the Test Plan and requests the next activity.

## Output shape

```text
## Test Plan for [Project Name]

1. Scope and Objectives
2. Testing Approach and Methodology
3. Test Phases and Activities
4. Test Scenarios and Coverage
5. Test Data and Environment
6. Test Schedule and Milestones
7. Roles and Responsibilities
8. Defect Management
9. Risks and Assumptions
10. Entry and Exit Criteria
11. Test Deliverables and Reporting

Gaps and Questions for the Author

--- HUMAN REVIEW GATE ---

Documents used:
Assumptions made:
Open questions:
Approval blockers:

"Approve or edit before I continue."
```

## Guadrails and security

- Never mark the plan as "final" - a human owns signoff.
- Never fabricate acceptance criteria; a missing AC is a finding, not a blank to fill.
- Keep scenarios traceable: each maps to a requirement, acceptance criterion or identified gap.
- Use the approved Test Strategy as the primary reference.
- Do not treat a draft Test Strategy as formally approved.
- Do not contradict approved Test Strategy requirements without identifying the conflict and asking for clarification.
- Do not invent business rules, test data, technical details or Jira content.
- Keep the workflow simple and avoid unnecessary documentation.
- Protect credentials, API tokens and sensitive production data.

## References

- `references/requirement-checklist.md` - the gap-analysis checklist.
- `references/testplan.md` - the Test Plan template.
- `requirements/example_test_plan.md` - optional organizational Test Plan example.
- `scripts/fetch_jira.sh` - Pull a ticket over the JIRA REST API when a Jira key is provided.
- `misc/mycompanydetails.md` - Organization-specific details.
- `copilot/test-plan.prompt.md` - the same skill as a GITHUB Copilot prompt file.

## Anti Hallucination rule

- Never assume anything. If you have any doubt or missing information, ask the user.
- Always use the approved Test Strategy as the primary input for Test Plan creation.
- Use BRD, Business Rules and STTM to understand and validate project requirements.
- Jira is optional. Do not make Jira mandatory when sufficient project documents are available.
- Never invent requirements, acceptance criteria, test data, expected results or technical details.
- If the Test Strategy and BRD contain conflicting information, ask the user before proceeding.
- Do not generate a Test Plan from an example template alone without actual project requirements.

## when not to use

Do not use it when:

- The user has not requested a Test Plan.
- No relevant project requirements or Test Strategy are available.
- The user only asks for a general explanation of ETL testing or Test Planning.
- The user requests a Test Strategy, detailed test cases, SQL scripts or automation instead of a Test Plan.
- The user wants to proceed without resolving essential requirement conflicts or missing information.

Do not require a Jira ticket when an approved Test Strategy and sufficient project requirements are available.