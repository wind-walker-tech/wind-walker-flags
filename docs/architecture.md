# Windwalker Flags – High-Level Architecture

This diagram reflects the **cloud- and auth-agnostic** direction. AWS (API Gateway, Lambda, DynamoDB, Cognito) is the **initial implementation**, but both **Auth** and **Data** layers are pluggable.

```mermaid
flowchart LR
  %% Clients and SDKs
  subgraph Clients
    C1[.NET Apps
NuGet .NET Standard 2.0]
    C2[React / Next.js Apps
@windwalker/flags-react]
    C3[Angular 15+
@windwalker/flags-angular]
    C4[AngularJS 1.x
windwalker-flags-angularjs]
    C5[Other Services / CLI]
  end

  %% API Layer
  subgraph API[GraphQL API Go]
    A1[Transport: REST/GraphQL over HTTP]
    A2[Resolvers & AuthZ Guard]
    A3[Evaluation Engine]
    A4[Repository Interface Data Access Abstraction]
  end

  %% Auth Providers (pluggable)
  subgraph Auth[Auth Provider Pluggable]
    direction TB
    P1[Cognito]
    P2[Okta]
    P3[Auth0]
    P4[Azure AD]
  end

  %% Data Providers (pluggable)
  subgraph Data[Data Store Pluggable]
    direction TB
    D1[(DynamoDB
Single Table)]
    D2[(PostgreSQL)]
    D3[(MongoDB)]
    D4[(Redis/Key-Value)]
  end

  %% AWS Initial Hosting (example)
  subgraph AWS[Initial Hosting]
    H1[API Gateway]
    H2[Lambda Go]
  end

  %% Flows
  C1 -->|JWT| H1 --> H2 --> A1
  C2 -->|JWT| H1
  C3 -->|JWT| H1
  C4 -->|JWT| H1
  C5 -->|JWT| H1

  A1 --> A2 --> A3 --> A4
  A2 <-->|OIDC/JWT| Auth
  A4 <-->|CRUD| Data

  %% Notes
  click D1 href "https://aws.amazon.com/dynamodb/" "DynamoDB"
  click P1 href "https://aws.amazon.com/cognito/" "Cognito"
```

**Legend**
- **Clients**: SDKs for .NET, React/Next.js, Angular, AngularJS (others can call the API directly).
- **API**: Go GraphQL service with a clear **Repository Interface** so the persistence layer is pluggable.
- **Auth**: Any OIDC/JWT-compliant provider (Cognito first; Okta/Auth0/Azure AD swappable).
- **Data**: Starts with **DynamoDB**; adapters for Postgres/Mongo/Redis can be added without changing clients.
- **AWS**: Initial hosting uses API Gateway + Lambda. Containerized or other hosting models can be introduced later.
