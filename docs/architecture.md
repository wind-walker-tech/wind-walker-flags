# High-Level Architecture

```mermaid
graph TD
  subgraph User Interface
    UI[Next.js Admin Portal]
  end

  subgraph API Layer
    GraphQL[GraphQL API (.NET or Node.js)]
  end

  subgraph Data Store
    DynamoDB[(DynamoDB Feature Flags Table)]
  end

  subgraph Auth
    Cognito[AWS Cognito User Pool]
  end

  UI -->|Auth| Cognito
  UI -->|CRUD| GraphQL
  GraphQL --> DynamoDB
  GraphQL --> Cognito
```