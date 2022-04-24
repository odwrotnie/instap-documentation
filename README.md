# Instap documentation

The real [Documentation](https://odwrotnie.github.io/instap-documentation/)

## Authentication

### JWT Token
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
