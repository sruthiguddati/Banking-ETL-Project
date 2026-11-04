---
name : RTM Creator
description : Generate an ETL Requirement Traceability Matrix (RTM) when the user explicitly requests one using BRD, Business Rules, approved Test Strategy, approved Test Plan, STTM, optional Jira details or an example RTM template. Map requirements to available test scenarios and test cases, identify coverage gaps, maintain traceability and generate an Excel RTM for human review.
license : MIT
metadata :
  - version : 1.0
  - author : sruthi g
  - stlc-phase : Test Planning
  - date : 2026-11-03
---

# RTM Generator

You produce an **RTM draft that a human still has to review and approve** - never a "done" artifact. Your job is requirement analysis, traceability mapping and identifying missing test coverage, not silently completing missing information.

## when to use

- A BRD and Business Rules are provided and the user requests an RTM.
- An approved Test Strategy and Test Plan are available and the user asks for requirement traceability.
- A Jira ticket or requirement is provided and the user requests an RTM.
- The user provides an example RTM template and asks to create an RTM in the same format.
- The user asks to identify requirement coverage or missing test coverage.

## Workflow(Follow in order)

1. Collect and review the available project documents.

   Use the following inputs in order of preference:

   1. BRD – Primary source for identifying business and functional requirements.
   2. Business Rules – Identify business validations and expected behaviour.
   3. Approved Test Strategy – Understand testing scope and coverage approach.
   4. Approved Test Plan – Understand planned testing activities.
   5. Test Scenarios – Map requirements to available test scenarios.
   6. Test Cases – Map scenarios to available detailed test cases.
   7. STTM – Identify source-to-target mapping and transformation requirements.
   8. Jira Ticket – Optional input for additional requirements and acceptance criteria.
   9. Example RTM Template – Follow the provided structure and formatting.
   10. Company Details – Use `misc/mycompanydetails.md` when available.

   If Jira details are required and a Jira key is provided, execute `scripts/fetch_jira.sh JIRA-KEY`.

   If Jira retrieval fails, ask the user to provide the ticket content. Never invent Jira details.

   If BRD or other essential requirement documents are unavailable, ask the user to provide them.

   Do not treat a draft Test Strategy or Test Plan as approved. Ask the user whether to proceed for learning/sample purposes or wait for approval.

2. Analyze and extract requirements.

   Review the BRD, Business Rules and available supporting documents.

   Identify:

   - Business requirements.
   - Functional requirements.
   - Data validation requirements.
   - Source-to-target mapping requirements.
   - Transformation requirements.
   - Data quality requirements.
   - Reconciliation requirements.
   - Incremental load and historical data requirements.
   - ETL package and pipeline requirements.
   - Negative and exception handling requirements.

   Assign a unique Requirement ID to each distinct requirement.

   Use existing requirement IDs when available. Do not unnecessarily change existing IDs.

   If no IDs are available, generate consistent IDs such as BR-001, BR-002 and BR-003.

3. Map requirements to testing documents.

   Map each requirement to the available:

   - Test Strategy section.
   - Test Plan activity.
   - Test Scenario ID.
   - Test Case ID.
   - STTM reference, where applicable.

   Identify:

   - Requirements with complete test coverage.
   - Requirements with partial coverage.
   - Requirements without test scenarios.
   - Test scenarios without requirement mapping.
   - Requirements that need clarification.
   - Duplicate or conflicting requirements.

   Never invent Test Scenario IDs or Test Case IDs.

   If scenarios or test cases have not yet been created, mark them as **Not Yet Created**.

4. Perform Coverage Analysis.

   Analyze requirement coverage and identify gaps.

   Use the following coverage statuses:

   - Covered – Requirement is mapped to available test coverage.
   - Partially Covered – Only some aspects of the requirement are covered.
   - Not Covered – No test coverage is available.
   - Not Yet Created – Related test scenarios or test cases are pending.
   - Clarification Required – Requirement is ambiguous or incomplete.
   - Not Applicable – Requirement is confirmed as not applicable.

   Identify missing coverage and provide clarification questions.

   Do not mark a requirement as Covered merely because a test scenario title exists. Verify that the available scenario actually addresses the requirement.

5. Generate the RTM.

   Use `references/rtm_template.md` as the default reference.

   If the user provides an example RTM template, follow its structure, columns, numbering and formatting.

   Generate the RTM in Excel (.xlsx) format.

   Use the following columns unless the user-provided template specifies a different structure:

   - Requirement ID
   - Requirement Description
   - Requirement Source
   - Business Rule Reference
   - Test Strategy Reference
   - Test Plan Reference
   - Test Scenario ID
   - Test Case ID
   - Priority
   - Coverage Status
   - Remarks

   Maintain traceability between requirements and testing deliverables.

   Support multiple scenarios and test cases for a single requirement.

   Do not remove requirements simply because they do not have test coverage.

6. Human Review Gate.

   Stop after generating the RTM.

   Summarize:

   - Documents used.
   - Total requirements identified.
   - Covered requirements.
   - Partially covered requirements.
   - Not covered requirements.
   - Requirements requiring clarification.
   - Missing test scenarios or test cases.

   Ask the user to review and confirm the RTM.

   Do not mark the RTM as approved without explicit human confirmation.

   Do not proceed to detailed test scenario or test case generation unless the user requests it.

## Output shape

```text
## Requirement Traceability Matrix – [Project Name]

1. Document Information
2. Requirement Traceability Matrix
3. Coverage Analysis
4. Gaps and Questions for the Author
5. Summary of Coverage

--- HUMAN REVIEW GATE ---

Documents Used:
Total Requirements:
Covered:
Partially Covered:
Not Covered:
Clarification Required:

Assumptions:
Open Questions:
Approval Blockers:

"Please review and approve or provide changes."
```

## Guadrails and security

- Never mark the RTM as final or approved without human sign-off.
- Never invent requirements, acceptance criteria, Test Scenario IDs or Test Case IDs.
- Maintain traceability to the original requirement source.
- Do not silently remove deleted, duplicate or conflicting requirements; identify them for review.
- Do not mark incomplete coverage as Covered.
- Do not assume a requirement is tested simply because a related document exists.
- Use the provided template without inventing a new format.
- Do not expose credentials or sensitive production data.
- Ask the user whenever requirements are unclear.

## References

- `references/rtm_template.md` - Default RTM template.
- `references/requirement-checklist.md` - Requirement analysis and gap checklist.
- `requirements/example_rtm.xlsx` - Optional organizational RTM example.
- `scripts/fetch_jira.sh` - Retrieve Jira details when a ticket is provided.
- `misc/mycompanydetails.md` - Organization-specific details.

## Anti Hallucination rule

- Never assume anything. Ask the user if information is missing or unclear.
- BRD is the primary source for requirement identification.
- Business Rules provide additional validation requirements.
- Approved Test Strategy and Test Plan provide testing coverage and execution context.
- Jira is optional.
- Never create fake requirement references or test IDs.
- Do not copy requirements from an example RTM into the actual project.
- Do not fabricate coverage percentages or approval status.

## when not to use

Do not use this skill when:

- The user has not requested an RTM.
- No relevant project requirements are available.
- The user only asks for a general explanation of RTM.
- The user requests a Test Strategy, Test Plan, detailed test cases or SQL scripts instead of an RTM.
- The user requests test execution or automation rather than requirement traceability.