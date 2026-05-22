# RBAC Permission Simulator

Built while studying Course 2 of the Google Cybersecurity Certificate 
— Play It Safe: Manage Security Risks.

## What it does
Simulates a basic Role-Based Access Control system.
- 4 roles: admin, developer, analyst, intern
- Each role has specific permitted actions
- Wrong key = access denied before permission check even runs
- Every attempt is logged as GRANTED or DENIED

## Concepts practiced
- Role-Based Access Control (RBAC)
- Principle of Least Privilege
- Authentication before authorization
- Access logging (like a basic SOC audit trail)

## How to run
python rbac_simulator.py

## Note
This is a learning project built to make IAM theory concrete.
Not production code.

