---
title: "Exploring the Next Frontier : Beyond CI/CD"
weight: 8
authors:
  - vijaywhat
---

In the world of online education for rural government school students, accessibility and quality are vital. Gurukulams.com is an online learning portal that provides affordable and effective education, driven by the dedication of our community. Built by students for students, 80% of our contributors have little to no prior experience in software development. This requires a codebase that is both simple and secure to encourage widespread participation.

## Our Approach

To ensure all contributors can engage effectively and securely, we implemented several key practices:

- **Checkstyle**: This tool enforces consistent coding standards, making it easier for new contributors to understand and contribute to the codebase.
- **ArchUnit**: ArchUnit ensures we follow architectural guidelines, keeping our system robust and scalable as new features are added.
- **JaCoCo**: We use JaCoCo for code coverage analysis to ensure our codebase is thoroughly tested, aiming for 100% coverage to minimize bugs.

## The Challenge

Despite following these CI/CD practices, we encountered an issue they couldn’t solve: technical debt from outdated dependencies and frameworks.

Our application, originally developed with Spring Boot 2, went through many changes. However, developers found it difficult to keep the codebase up-to-date with new versions. Many were not concerned with upgrades, leading to significant technical debt—a daunting challenge.

Think about it like this: When your phone gets a new Android update, you usually upgrade without hesitation. But in software development, developers often look for reasons not to upgrade, citing potential disruptions or the effort involved.

The core issue is that developers only upgrade when necessary. Regular and proactive updates are crucial to maintaining a healthy, secure, and efficient codebase.

## Our Solution

To address technical debt and keep our codebase up-to-date, we implemented these steps:

1. **Automated Dependency Updates**: We use the Maven Versions plugin with its "Upgrade" goal. It checks for the latest versions of our dependencies. If it finds updates, it creates a backup file named `pom.xml.bak` and updates the `pom.xml` file with the new versions.
  
2. **Build Failure on Pending Upgrades**: To enforce these updates, we use the Maven Enforcer plugin. It checks for the existence of the `pom.xml.bak` file. If this file is found, indicating pending upgrades, the build will fail. This ensures updates are addressed promptly.

To manage exceptions and allow specific dependencies to be excluded from upgrades when necessary, we can configure exclusions. This flexibility ensures critical or incompatible updates can be managed without stopping the entire upgrade process.

By taking these steps, we ensure our codebase stays current and secure, preventing technical debt from becoming a barrier to progress.
