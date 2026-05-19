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
def check_access(user_role):
    allowed_actions = {
        'admin': ['create', 'read', 'delete'], 
        'developer': ['create', 'read'],
        'intern': ['read']      
    }
    
    if user_role in allowed_actions:
        actions = allowed_actions[user_role]
        return f"User role '{user_role}' has access to: {', '.join(actions)}."  
    else:
        return f"User role '{user_role}' is not recognized. No access granted."
        
if __name__ == "__main__":
    role_input = input("Enter user role (admin/developer/intern): ").strip().lower()
   
    result = check_access(role_input)

    print("\n" + result)
```
