# Loan Repayment Workflow

This project implements a simple loan repayment workflow using DAML. It demonstrates the creation of loan limits, repayment restrictions, token issuance, loan requests, and repayments.

## Project Structure

- `LoanWorkflow.daml`: Contains the main templates and choices for the loan workflow.
- `Main.daml`: Includes the setup script to demonstrate the workflow.
- `Test.daml`: Contains a test script that runs the setup.

## How to Run

1. Ensure you have DAML SDK installed (version 2.9.4 or compatible).
2. Clone this repository.
3. Navigate to the project directory.
4. Run the following commands:

```bash
# Start the DAML sandbox
daml start

# Run the setup script
daml script --dar .daml/dist/loan-repayment-workflow-0.1.0.dar --script-name Main:setup

# Run the test script
daml test
```

## Sample Output Logs

When you run the setup script, you should see output similar to the following:

```
Created LoanLimit contract with ID: #124:0
Created RepaymentRestriction contract with ID: #125:0
Created Token contract with ID: #126:0
Created Loan contract with ID: #127:0
Queried Loan contract: Loan(bank = 'Bank', customer = 'Alice', amount = 5000.0, repaid = 0.0)
After first repayment, new LoanLimit contract ID: #128:0
Queried Loan contract after first repayment: Loan(bank = 'Bank', customer = 'Alice', amount = 5000.0, repaid = 2000.0)
After second repayment, final LoanLimit contract ID: #129:0
Loan contract should be archived now
Final LoanLimit contract: LoanLimit(bank = 'Bank', customer = 'Alice', limit = 10000.0, utilized = 0.0)
```

This output demonstrates the creation of contracts, loan requests, repayments, and the final state of the loan limit after full repayment.

## Workflow Explanation

1. A `LoanLimit` is created for Alice by the Bank.
2. A `RepaymentRestriction` is set for Alice.
3. A `Token` is issued to Alice by the Bank.
4. Alice requests a loan using her token.
5. Alice makes a partial repayment.
6. Alice makes a final repayment, fully repaying the loan.
7. The loan is archived, and the loan limit is updated to reflect full repayment.

This workflow demonstrates the full lifecycle of a loan, from issuance to full repayment, including the handling of tokens and repayment restrictions.
