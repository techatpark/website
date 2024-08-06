---
title: "Exploring the Next Frontier : Beyond CI/CD"
weight: 8
authors:
  - vijaywhat
---

[Gurukulams](https://gurukulams.com/) is an online learning portal that provides affordable and effective education platform, developed by students for students, 80% of our contributions come from people with little to no prior experience in software development. This requires a codebase that is both simple and secure to encourage widespread participation.

## Our Approach

To ensure all contributors can engage effectively and securely, we implemented several key practices:

- Enforce consistent **coding standards**, making it easier for new contributors to understand and contribute to the codebase. (**Checkstyle**)
- Ensure we follow **architectural guidelines**, keeping our system robust and scalable as new features are added. (**ArchUnit**)
- Ensure our **codebase is thoroughly tested**, aiming for **100% coverage** to minimize bugs. (**JaCoCo**)

with all this we expected that we have happy ending. but wait :). we were in for a surprise with an unexpected challenge.

## The Challenge

Despite following these CI/CD practices, we encountered an issue they couldn’t solve: technical debt from old version of dependencies and frameworks.

Our application, originally developed with Spring Boot 2, went through many changes. However, developers found it difficult to keep the codebase up-to-date with new versions. Many were not concerned with upgrades, leading to significant technical debt—a daunting challenge.

Consider that, you receive a new Android update on your phone, you typically upgrade without hesitation, understanding the benefits it brings and the potential issues it fixes. However, in software development, the mindset often shifts. Developers frequently question why they should upgrade, focusing on potential disruptions or the effort required, rather than proactively seeking improvements.

The core issue is that developers tend to upgrade only when absolutely necessary. In contrast, regular and proactive updates are essential for maintaining a healthy, secure, and efficient codebase. Shouldn’t the approach be the opposite, where we seek reasons to upgrade rather than reasons to delay?

## Our Solution

To address technical debt and keep our codebase up-to-date, we implemented these steps:

1. **Automated Dependency Updates**: We use the [Maven Versions](https://www.mojohaus.org/versions/versions-maven-plugin/index.html) plugin with its "Upgrade" goal. It checks for the latest versions of our dependencies. If it finds updates, it creates a backup file named `pom.xml.versionsBackup` and updates the `pom.xml` file with the new versions.

```sh
mvn versions:update-parent versions:update-properties
```
  
2. **Build Failure on Pending Upgrades**: To enforce these updates, we use the [Maven Enforcer](https://maven.apache.org/enforcer/maven-enforcer-plugin/usage.html) plugin. It checks for the existence of the `pom.xml.versionsBackup` file. If this file is found, indicating pending upgrades, the build will fail. This ensures updates are addressed promptly.

```sh
mvn clean package
```

3. **To manage exceptions**: Allow specific dependencies to be excluded from upgrades when necessary, we can configure exclusions. This flexibility ensures critical or incompatible updates can be managed without stopping the entire upgrade process.

## Lessons Learned

By taking these steps, we ensure our codebase stays current and secure, preventing technical debt from becoming a barrier to progress. However, this approach is not without its challenges and resistance.

1. **Typical question from Product/business people**: "When my application is working, why do I need to upgrade to the latest version of technologies/libraries?"
   
   **Answer**: Business functionalities might work, but upgrades offer:
   - Fixing security vulnerabilities
   - Performance improvements
   - Cost effectiveness (continuous upgrades cost less than big upgrades)
   - Minimal tech debt

2. **Doesn't these upgrades incur time and effort (cost)?**
   
   **Answer**: Yes, but the cost is minimal with continuous upgrades compared to bigger upgrades.
   - Bigger upgrades are like mountains. Climbing a mountain in one shot is challenging. Similarly, big upgrades require significant time and money.
   - Frequent upgrades are like steps up the mountain. Regular upgrades make reaching the summit easier, with only a little extra effort and cost needed.

3. **Known Limitations**
   - Maven coordinate changes are not handled.
   - Created developer ambiguity. Work is in progress to find the differences and communicate them to developers.




