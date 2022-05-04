# Instap documentation

User [Documentation](https://odwrotnie.github.io/instap-documentation/)

## Contexts

Each **user** is assigned to a **context**. In specific cases user can switch to another **context**.


```mermaid
classDiagram

Context <-- Definition
Definition<--Item
Context <-- Item
```

- Definition's context == null (global definition)
  - Item's context != null (accessible only in selected context)
  - Item's context == null (accessible in all contexts)
- Definition's context == X
  - Item's context == null (accessible only in context X)
  - Item's context == X (accessible only in context X)
  - Item's context == Y (accessible only in context X)
  
## Authentication

The **S** can be one of each:
- Setup
- CRON LDAP
- Calculations

```mermaid
graph TD;
    Client---Proxy;
    Proxy---Auth;
    Proxy---S;
    S---Auth
    Proxy---Definitions;
    Definitions---Auth;
    Proxy---Items;
    Items---Auth;
```

**JWT Token** consists of:
- roles: List[String]

```mermaid
sequenceDiagram

User->>Auth:Get token (by username and password)
Auth->>User:JWT Token
Note left of User: Now, User has<br/>its JWT Token<br/>with his roles
User->>A Service:A method (with JWT Token that has roles)
A Service->>Auth:Ask about permissions for roles if not cached
Auth->>Items:Get permissions for roles
Items->>Auth:Permissions for roles
Auth->>A Service:Permissions for roles
A Service->>User:Result

```
