# 🔍 Role Permissions Enumerator (Python)

A lightweight security script designed to audit and display the complete permission profile of an identity container. This utility simulates the discovery phase of an Identity and Access Management (IAM) evaluation, mapping roles to their authorized systemic capabilities.

---

## 🎯 Project Overview
In large enterprise environments, security analysts frequently need to audit roles to ensure compliance with the **Principle of Least Privilege (PoLP)**. This tool automates that assessment locally by accepting a target organizational role, verifying its presence within the authorization schema, and extracting all associated operations.

### Key Security & Coding Mechanisms:
* **Clearance Enumeration:** Dynamically strings together separate arrays of permissions into a single, comma-separated list using Python's string joining logic.
* **Input Hardening:** Utilizes `.strip()` to slice off accidental trailing spaces and `.lower()` to sanitize the input vector against case-mismatch bypass errors.
* **Constant-Time Mapping:** Leverages a dictionary key lookup algorithm ($O(1)$ complexity) to locate the target authorization block without scanning the entire structural model.

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
