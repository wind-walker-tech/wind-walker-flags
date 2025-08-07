# Data Model

```mermaid
erDiagram
  FeatureFlag ||--o{ EnvironmentFlag : contains
  EnvironmentFlag ||--o{ TargetingRule : includes

  FeatureFlag {
    string flagId PK
    string name
    string description
    string createdAt
  }

  EnvironmentFlag {
    string flagId FK
    string environment (dev|qa|stage|prod)
    boolean enabled
    float rolloutPercentage (optional)
    string updatedAt
  }

  TargetingRule {
    string ruleId PK
    string flagId FK
    string environment
    string type (user|org|custom)
    string conditionJson
    string createdBy
  }
```