Design and implement a new “Service Intelligence” page inside our existing TypeScript application.

Requirements:
- Integrate into the existing codebase and match the current UI/theme exactly.
- Reuse existing layout, components, styles, and navigation patterns.
- Add a top nav button to open the new page.
- Do not build a standalone app or a visually separate experience.

Page features:
- Support Redis, Elasticsearch, Kafka, and similar services.
- Show clusters vs. instances and their versions.
- Show upgrade notices driven by CVEs, patches, and major features.
- Show release notes, patch notes, latest changes, and version comparisons.
- Show service-specific CVEs and advisories.
- Prepare for vendor API integrations for support and incident workflows.
- Include AI-assisted summaries, comparisons, and upgrade guidance.

Backend context:
- Python backend.
- Discover services and versions from OpenShift.
- Pull release and CVE data from external/vendor sources.
- Use placeholder/mock data if live integrations are incomplete.

Please return:
- integration plan,
- frontend architecture,
- UI plan matched to current app patterns,
- backend/data plan,
- phased rollout plan,
- and implementation guidance aligned with the existing codebase.
