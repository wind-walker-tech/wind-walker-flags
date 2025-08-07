# 🌬️ Windwalker Flags

**Windwalker Flags** is a lightweight, AWS-native, cross-platform feature flag service built for modern application stacks. It supports .NET 8+, .NET Framework 4.8, GraphQL APIs, and a React/Next.js UI — all designed with consulting clients and reusable deployment in mind.

---

## 🚀 Features

- ✅ Works with both .NET 8+ and .NET Framework 4.8 (via NuGet wrapper)
- ✅ Centralized feature flags stored in DynamoDB
- ✅ GraphQL API for full CRUD and evaluation
- ✅ React/Next.js Admin UI secured with AWS Cognito
- ✅ Environment-specific flags (`dev`, `qa`, `stage`, `prod`)
- ✅ Support for user/org-specific targeting
- ✅ MIT Licensed and client-friendly for commercial use

---

## 🧱 Project Structure

```text
windwalker-flags/
├── api/              # GraphQL API for managing & evaluating flags
├── ui/               # Next.js admin portal
├── packages/
│   ├── dotnet-core/  # .NET 8+ feature flag integration
│   └── dotnet-fx/    # .NET Framework NuGet package
├── infrastructure/   # IaC templates (Serverless Framework or SAM)
└── docs/             # Diagrams and setup guides
```

---

## 🛠 Tech Stack

| Layer        | Tech                     |
|--------------|--------------------------|
| Data Store   | AWS DynamoDB             |
| API          | GraphQL (via .NET or Node) |
| UI           | React / Next.js          |
| Auth         | AWS Cognito              |
| .NET Core    | Microsoft.FeatureManagement-compatible |
| .NET Framework | Custom NuGet client     |

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

---
