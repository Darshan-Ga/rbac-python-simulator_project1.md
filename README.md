# 🛡️ Role-Based Access Control (RBAC) Simulator

A lightweight Python command-line application that simulates an Identity and Access Management (IAM) policy engine. This project demonstrates how modern cloud architecture enforces security policies and the **Principle of Least Privilege (PoLP)**.

---

## 🎯 Project Overview

This script acts as a security gatekeeper. It accepts a user's role and a requested action, processes the input through a multi-tier conditional logic matrix, and evaluates whether to grant access, deny access based on insufficient permissions, or flag an invalid identity container.

### Key Security Concepts Implemented:
* **Role-Based Access Control (RBAC):** Grouping permissions by systemic roles (`admin`, `developer`, `intern`) rather than individual accounts.
* **Principle of Least Privilege (PoLP):** Users are restricted to the bare minimum permissions required to perform their tasks (e.g., an `intern` can only `read`).
* **Input Sanitization:** Enforces data uniformity by normalizing inputs using `.lower()` to avoid casing bypass vulnerabilities.

---

## 🧠 How It Works Under the Hood

### 1. The Policy Matrix (Hash Table Lookup)
The permission structure is mapped using a Python dictionary. At the system level, this functions as a hash table, allowing the system to verify roles in **$O(1)$ constant time** execution complexity.

---

## 💻 Source Code

```python
def check_access(user_role, action):
    allowed_actions = {
        'admin': ['create', 'read', 'delete'], 
        'developer': ['create', 'read'],
        'intern': ['read']      
    }
    
    if user_role in allowed_actions and action in allowed_actions[user_role]:
        return f"permission_granted: {user_role.upper()} permitted to {action.upper()}"
    elif user_role in allowed_actions:
        return f"permission_denied: {user_role.upper()} not permitted to {action.upper()}"
    else:
        return f"invalid_role: {user_role.upper()} is not a recognized role"


if __name__ == "__main__":
    role_input = input("Enter user role (admin/developer/intern): ").lower()
    action_input = input("Enter action (create/read/delete): ").lower()

    result = check_access(role_input, action_input)

    print("\n" + result)
