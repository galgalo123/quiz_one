# Campus Access & Safety Rules - Knowledge-Based System

## Student Information
- **Name:** Galgalo Molu Halake
- **Registration Number:** 669377
- **Course:** APT3020B

## Project Description
This project implements a rule-based Knowledge-Based System (KBS) using forward chaining inference to determine campus access decisions. The system evaluates a student's eligibility to enter campus based on various facts and applies logical rules to make an automated decision.

The KBS stores facts about students (such as identification, registration status, fee payment, and health clearance) and applies rules to infer new knowledge, ultimately determining whether campus entry should be granted or denied.

## How to Run
1. Open the `kbs_quiz.ipynb` notebook in Jupyter Notebook, JupyterLab, or VS Code
2. Run all cells sequentially (Cell → Run All, or click "Run All" button)
3. Observe the outputs showing:
   - Initial facts
   - Rule application
   - Newly inferred facts
   - Final decision

## Facts Used
The knowledge base uses the following initial facts:

1. `has_student_id` - Student possesses a valid student ID card
2. `is_registered_student` - Student is officially registered for the current term
3. `has_paid_fees` - Student has completed fee payment
4. `has_health_clearance` - Student has valid health clearance certificate

## Rules (IF-THEN Format)

### Single-Condition Rules:
1. **IF** has_student_id **THEN** identity_confirmed
2. **IF** has_health_clearance **THEN** health_verified

### Multi-Condition Rules:
3. **IF** identity_confirmed **AND** is_registered_student **THEN** is_verified_student
4. **IF** is_verified_student **AND** has_paid_fees **THEN** financial_clearance_granted

### Chained Rules:
5. **IF** financial_clearance_granted **AND** health_verified **THEN** access_requirements_met
6. **IF** access_requirements_met **THEN** campus_entry_granted

## Final Decision Logic
The final decision is based on the presence of the `campus_entry_granted` fact:

- **ENTRY GRANTED**: If `campus_entry_granted` exists in the knowledge base after inference
- **ENTRY DENIED**: If `campus_entry_granted` does NOT exist in the knowledge base

The system uses forward chaining, meaning rules are applied iteratively until no new facts can be inferred. For entry to be granted, all requirements must be satisfied through the chain of rules.

## System Architecture

### Knowledge Representation
- **Facts**: Stored as a Python `set` for efficient lookup and uniqueness
- **Rules**: Stored as a `list` of dictionaries, each containing:
  - `condition`: A lambda function that checks if rule conditions are satisfied
  - `conclusion`: A string representing the fact to be inferred

### Inference Engine
The `infer()` method implements forward chaining:
1. Iterates through all rules
2. Checks if each rule's condition is satisfied by current facts
3. Adds conclusions of satisfied rules as new facts
4. Repeats until no new facts can be inferred (fixed point reached)

## Test Cases
The notebook includes two scenarios:

1. **Entry Granted**: All requirements met (ID, registration, fees, health clearance)
2. **Entry Denied**: Missing health clearance, demonstrating the system correctly denies access when requirements are incomplete

## Key Features
- ✅ Forward chaining inference engine
- ✅ 4+ initial facts
- ✅ 6 rules (including single-condition, multi-condition, and chained)
- ✅ Automated decision making
- ✅ Complete audit trail of inferred facts
- ✅ Test scenarios for both grant and denial outcomes

## File Structure
```
kbs-practical-quiz/
├── kbs_quiz.ipynb    # Main notebook with KBS implementation
└── README.md         # This file
```

## Requirements
- Python 3.x
- Jupyter Notebook (or JupyterLab/VS Code with Jupyter extension)

No external libraries required - uses only Python standard library.
