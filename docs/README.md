# 📚 Windwalker Flags Documentation

This folder contains the **design, architecture, and setup documentation** for the Windwalker Flags project.

> We’ve restored the full diagrams here for quick reference and kept a deeper **pluggable architecture** view in [`architecture.md`](./architecture.md).

---

## 1) System Architecture (High Level)

```mermaid
flowchart LR
  subgraph AWS
    APIGW[API Gateway]
    L[Lambda: Go GraphQL]
    DDB[(DynamoDB: Feature Flags)]
    COG[Cognito: User Pool + Groups\nadmin, developer]
  end

  Clients[.NET SDK / React SDK / Angular / AngularJS] -->|JWT OIDC| APIGW
  APIGW <--> L
  L <--> DDB
```

**Legend**
- **Clients**: SDKs for .NET Standard 2.0, React/Next.js, Angular, AngularJS.
- **API Gateway**: Public entrypoint; routes to Lambda.
- **Lambda (Go GraphQL)**: Business logic, authZ guards, evaluation.
- **DynamoDB**: Single-table design for flags, env states, rules, logs.
- **Cognito**: Initial auth provider (swappable via OIDC/JWT).

➡ See also: [`architecture.md`](./architecture.md) for **pluggable Auth (Cognito/Okta/Auth0/Azure AD)** and **pluggable Data (DynamoDB/Postgres/Mongo/Redis)** diagrams.

---

## 2) Data Model

### Logical Model
```mermaid
classDiagram
    class FeatureFlag {
      +string Id
      +string Name
      +string? Description
      +datetime CreatedAt
    }

    class EnvironmentFlag {
      +string FlagId
      +enum Environment  DEV, QA, STAGE, PROD 
      +bool Enabled
      +float? RolloutPercentage
      +datetime UpdatedAt
      +string UpdatedBy
    }

    class TargetingRule {
      +string Id
      +string FlagId
      +enum Environment
      +enum Type  USER, ORG, ADVANCED 
      +string Condition
      +datetime CreatedAt
      +string CreatedBy
    }

    class ChangeLogEntry {
      +string Id
      +string FlagId
      +datetime Timestamp
      +string Actor
      +string Action
      +string? BeforeJson
      +string? AfterJson
    }

    FeatureFlag "1" --> "0..4" EnvironmentFlag : has
    FeatureFlag "1" --> "0..*" TargetingRule : scoped-to-env
    FeatureFlag "1" --> "0..*" ChangeLogEntry : audited
```

### Physical (DynamoDB Single Table)
```mermaid
flowchart TB
  subgraph DynamoDB Single Table
    direction TB
    A[FLAG#<flagId> + SK= META
      ---
      Name, Description, CreatedAt]

    B[FLAG#<flagId> + SK= ENV#<ENV>
      ---
      Enabled, Rollout%, UpdatedAt, UpdatedBy
      GSI1PK=ENV#<ENV>, GSI1SK=FLAG#<flagId>]

    C[FLAG#<flagId> + SK= ENV#<ENV>#RULE#<ruleId>
      ---
      Type, Condition, CreatedAt, CreatedBy]

    D[FLAG#<flagId> + SK= LOG#<ticks>
      ---
      Actor, Action, BeforeJson, AfterJson]
  end
```

**Notes**
- **PK/SK**: `PK=FLAG#<id>`, `SK` in `{META, ENV#<ENV>, ENV#<ENV>#RULE#<ruleId>, LOG#<ticks>}`
- **GSI1**: `GSI1PK=ENV#<ENV>`, `GSI1SK=FLAG#<id>` for “flags by environment”

---

## 3) CI/CD Pipeline (GitHub Actions → SAM → Prod)

```mermaid
flowchart LR
  Dev[Developer] -->|branch + commits| GH[GitHub Repo]

  GH --> PR[Open Pull Request]
  PR --> CI1[Job: Lint & Unit Tests\nGo build ./... & go test ./...]
  CI1 --> CI2[Job: GraphQL Checks\nschema snapshot, gql queries compile]
  CI2 --> CI3[Job: Package Lambda\nGOOS=linux build → zip artifact]
  CI3 -->|artifact| Gate[Manual Review/Approval]

  Gate --> Merge[Merge to main]
  Merge --> CD1[Job: SAM Package\nsam package → S3]
  CD1 --> CD2[Job: SAM Deploy prod\ncapabilities: CAPABILITY_NAMED_IAM]
  CD2 --> Post[Post-Deploy Tasks\noutputs → GH env vars\noptional seed script]

  subgraph AWS Prod
    APIGW[API Gateway]
    L[Lambda: Go GraphQL]
    DDB[(DynamoDB: flags)]
    COG[Cognito: User Pool + Groups\nadmin, developer]
  end

  CD2 --> APIGW
  CD2 --> L
  CD2 --> DDB
  CD2 --> COG

  APIGW <--> L
  L <--> DDB
  Clients[.NET / React / Angular / AngularJS] -->|JWT OIDC| APIGW
```

---

## Developer Guides

- Setting up the development environment
- Building and testing the GoLang API
- Adding new feature flags
- Managing role-based access for flag control

(Coming soon in this folder as separate guides.)

---

## SDK Documentation

- .NET Standard 2.0 SDK (works with .NET 8+ and .NET Framework 4.8)
- React/Next.js SDK
- Angular SDK
- AngularJS SDK

(Each SDK will have its own README under `/packages`.)

---

## Infrastructure

- AWS SAM templates for deploying the API
- Future multi-cloud deployment strategy

---

## UI

- Admin UI in React/Next.js
- Angular admin UI (planned)
