# RTM Creator

## Metadata
- Name: RTM Creator
- Description: Creates an ETL Requirements Traceability Matrix by mapping business requirements to test strategy, test plan, test scenarios and test cases.
- Version: 1.0
- Author: Sruthi
- Document Type: Requirements Traceability Matrix

## Purpose
Create a complete and accurate Requirements Traceability Matrix (RTM) for ETL testing projects. Ensure every business requirement is traceable to the corresponding testing activities and test cases.

## When to Use
Use this skill when:
- The user explicitly requests RTM creation.
- Business Requirements Document (BRD) is provided.
- Business Rules are available.
- Test Strategy and Test Plan are available.
- Test Scenarios and Test Cases are available.

## Input Documents
1. Business Requirements Document (BRD) – Primary requirement source.
2. Business Rules – Business validations and processing rules.
3. Approved Test Strategy – Testing approach and coverage.
4. Approved Test Plan – Testing activities and execution scope.
5. Source-to-Target Mapping (STTM) – Source and target field mappings.
6. Test Scenarios – Scenario-level traceability.
7. Test Cases – Detailed test coverage.
8. Jira requirements – Optional.

Do not assume missing requirements or invent test case IDs.

## Workflow

### Step 1: Analyze Inputs
- Read all supplied documents.
- Extract functional and non-functional requirements.
- Identify business rules.
- Identify unique requirement IDs.
- Identify missing or ambiguous requirements.

### Step 2: Requirement Mapping
Map each requirement to:
- Business Rule Reference
- Test Strategy Reference
- Test Plan Reference
- Test Scenario ID
- Test Case ID
- STTM Reference, wherever applicable.

### Step 3: Coverage Analysis
Evaluate whether each requirement is fully covered, partially covered or not covered.

Use the following statuses:
- Covered
- Partially Covered
- Not Covered
- Not Yet Created
- Clarification Required
- Not Applicable

Do not mark a requirement as Covered merely because a test scenario exists. Verify the actual test coverage.

### Step 4: Generate RTM

Create the RTM with the following columns:

| Column | Description |
|---|---|
| Requirement ID | Unique business requirement identifier |
| Requirement Description | Requirement details |
| Requirement Source | BRD or other source |
| Business Rule Reference | Related business rule |
| Test Strategy Reference | Related strategy section |
| Test Plan Reference | Related test plan section |
| Test Scenario ID | Related scenario identifier |
| Test Case ID | Related test case identifier |
| Priority | P0 / P1 / P2 / TBD |
| Coverage Status | Coverage assessment |
| Remarks | Gaps or clarification notes |

### Step 5: Validation
- Verify every requirement is mapped.
- Identify requirements without test coverage.
- Identify test cases without requirement references.
- Verify traceability