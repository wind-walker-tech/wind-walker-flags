# Feature Flag Service Story Map

This story map organizes user stories by major epics (rows) and separates MVP features from follow-up releases (columns).

    %% Story map grouped by epics (rows) and releases (columns)
    graph LR
        subgraph MVP
            BackendAPI["Backend API\n• Go GraphQL schema\n• EvaluateFlag resolver"]
            DotNetSDK[".NET SDK\n• .NET Standard 2.0\n• IsEnabled() API"]
            ReactSDK["React/Next.js SDK\n• Core TS client\n• Integration"]
            UI["Admin UI\n• Create/edit flags\n• Role‑based toggle"]
            Auth["Auth Provider\n• Default Cognito integration"]
        end
        subgraph Next Releases
            AngularSDK["Angular SDK\n• Injectable service\n• Observables"]
            AngularJSSDK["AngularJS SDK\n• $windwalkerFlags service"]
            PluggableData["Pluggable Datastore\n• Repo interface\n• New drivers"]
            PluggableAuth["Pluggable Auth\n• Okta/Auth0/Azure AD support"]
            UsageAnalytics["Usage & Rollout\n• % rollouts\n• Analytics & logs"]
        end

        BackendAPI --> AngularSDK
        BackendAPI --> AngularJSSDK
        BackendAPI --> PluggableData
        DotNetSDK --> PluggableAuth
        ReactSDK --> UsageAnalytics
        UI --> PluggableAuth
