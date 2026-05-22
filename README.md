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
---

## 💻 Source Code

```python
access_log = []
role_keys = {
    'admin': 'admin123',
    'developer': 'dev456',
    'analyst': 'analyst789',
    'intern': 'intern000'
    }
def check_access(user_role,action):
    allowed_actions = {
        'analyst': ['read', 'view_logs'],
        'admin': ['create', 'read', 'delete'], 
        'developer': ['create', 'read'],
        'intern': ['read']      
    }
    
    if user_role in allowed_actions:
        actions = allowed_actions[user_role]
        if action in actions:
          access_log.append(f"{user_role} | {action} | GRANTED")
          return f"User role '{user_role}' has access to: {action}."  
        else:
          access_log.append(f"{user_role} | {action} | DENIED")
          return f"ACCESS DENIED — '{user_role}' cannot perform '{action}'. Allowed: {', '.join(actions)}."
    else: 
        access_log.append(f"{user_role} | {action} | DENIED-unknown_role")
        return f"ACCESS DENIED — '{user_role}' is not a recognized role."    

if __name__ == "__main__":
    username = input("Enter username: ").strip()
    role_input = input("Enter user role (admin/developer/intern/analyst): ").strip().lower()
    action_input = input("Enter action (create/read/delete/view_logs): ").strip().lower()
    key_input = input("Enter access key: ").strip()

    if role_keys.get(role_input) == key_input:
          result = check_access(role_input, action_input)
    else:
          result = "ACCESS DENIED — invalid role key."
          access_log.append(f"{username} | {role_input} | INVALID KEY")

    print(f"\n{username} | {result}")

    print("\n--- Access Log ---")
    for entry in access_log:
       print(entry)
```
