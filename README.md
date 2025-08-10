# 🌬️ Windwalker Flags

**Windwalker Flags** is a lightweight, AWS-native, cross-platform feature flag service built for modern application stacks.  
It is designed to be **cloud-agnostic** and **auth-agnostic**, starting with AWS DynamoDB + AWS Cognito but with planned support for alternate datastores (e.g., PostgreSQL, MongoDB) and authentication systems (e.g., Okta, Auth0, Azure AD).

---

## 🚀 Features

- ✅ Works with both .NET 8+ and .NET Framework 4.8 (via single **.NET Standard 2.0** NuGet package)
- ✅ React/Next.js SDK
- ✅ Angular SDK
- ✅ AngularJS SDK
- ✅ Centralized feature flags stored in DynamoDB (pluggable backend planned)
- ✅ GoLang-based GraphQL API for full CRUD and evaluation
- ✅ React/Next.js Admin UI (Angular admin planned) secured with AWS Cognito (auth provider swappable)
- ✅ Environment-specific flags (`dev`, `qa`, `stage`, `prod`)
- ✅ Support for user/org-specific targeting
- ✅ MIT Licensed and client-friendly for commercial use

---

## 🧱 Project Structure

```text
windwalker-flags/
├── api/              # GraphQL API (GoLang) for managing & evaluating flags
├── ui/               # Next.js admin portal
├── packages/
│   ├── dotnet/       # .NET Standard 2.0 SDK for .NET 8+ and .NET Framework 4.8
│   ├── react/        # React/Next.js SDK
│   ├── angular/      # Angular SDK
│   └── angularjs/    # AngularJS SDK
├── infrastructure/   # IaC templates (AWS SAM / CloudFormation)
└── docs/             # Diagrams and setup guides
```

---

## 🛠 Tech Stack

| Layer        | Tech                                                   |
|--------------|--------------------------------------------------------|
| Data Store   | AWS DynamoDB (pluggable datastore planned)              |
| API          | GoLang + GraphQL                                        |
| UI           | React / Next.js (Angular planned)                       |
| Auth         | AWS Cognito (swappable with Okta, Auth0, Azure AD, etc.)|
| SDKs         | .NET Standard 2.0, React/Next.js, Angular, AngularJS    |

---

## 📊 Feature Comparison

| Feature                                | Windwalker Flags | LaunchDarkly | Split.io |
|----------------------------------------|------------------|--------------|----------|
| Multi-environment flags                | ✅               | ✅           | ✅       |
| Role-based production flag control     | ✅               | ✅           | ✅       |
| Cloud-agnostic design                  | 🔄 Planned       | ❌           | ❌       |
| Auth provider agnostic                 | 🔄 Planned       | ❌           | ❌       |
| .NET Standard 2.0 SDK                  | ✅               | ❌           | ❌       |
| React/Next.js SDK                      | ✅               | ✅           | ✅       |
| Angular SDK                            | ✅               | ✅           | ✅       |
| AngularJS SDK                          | ✅               | ❌           | ❌       |
| GoLang backend                         | ✅               | ❌           | ❌       |
| Self-hosted                            | ✅               | ❌           | ❌       |
| Free / MIT License                     | ✅               | ❌           | ❌       |

---

## 📦 Installation & Setup

🧪 Detailed setup guides will be provided in the `/docs` folder soon.

In the meantime, check out the open issues to follow development progress!

---

## 🤝 Contributing

This project is maintained by [Lister Potter](https://github.com/lister-potter).  
If you'd like to contribute or use Windwalker Flags in your consulting work, feel free to fork, clone, and submit PRs.

---

## 📄 License

This project is licensed under the **MIT License** — use it freely in commercial or personal projects.
