---
title: "Introducing SJSON: A Tailor-Made and Hackable JSON Parser for Optimized API Development"
weight: 2
authors:
  - VIJAYWHAT
tags:
  - JSON, Java
authorimage: 'https://avatars.githubusercontent.com/u/89501520?v=4'
---

# Introduction

During a casual discussion at the Bangalore Java User Group, the topic of JSON parsers sparked a debate on their pros and cons. This led to the inception of an innovative idea – creating yet another JSON parser, one that is tailor-made and hackable to cater specifically to the needs of API development. In this blog post, we'll delve into the reasons behind the creation of **SJSON** and explore its unique features.

## Tailor-Made for API Servers

In the realm of Java development, we are accustomed to using popular JSON parsers like Org JSON, Jackson, and Gson for various purposes. However, these parsers serve a broad spectrum of applications, including text editors, databases, and API servers. **SJSON** sets itself apart by focusing exclusively on the needs of API servers.

## Why Another Parser?

Unlike text editors that use JSON parsers to pinpoint errors, API servers typically only require a simple validation – is the JSON data valid or not? **SJSON** aligns with this need, avoiding the complexity of detailed error reporting. Moreover, unlike databases that perform querying on JSON data, API servers don't require such functionality. Hence, a specialized parser for API servers makes sense.

## Hackable for Custom Rules

One of the standout features of **SJSON** is its hackability. Consider a scenario where a standard JSON parser accepts keys with special characters, such as emojis. In an API server environment, however, you may want stricter rules, such as allowing only alphanumeric keys.

```json
{
  "ace": "Vijay",
  "efg": "I am emojey key"
}
```

'SJSON' empowers developers to define custom rules for keys, ensuring better security, improved performance, and the flexibility to extend data workflows according to specific project requirements.

## Get Involved on GitHub
We're excited to announce that 'SJSON' is an open-source project available on GitHub. We invite developers and the community to explore the code, provide feedback, and contribute to making 'SJSON' even more robust.

[Explore SJSON on GitHub](https://github.com/techatpark/sjson)

## Conclusion
In summary, 'SJSON' is not just another JSON parser – it's a specialized tool crafted for API servers, offering simplicity in error validation and hackability for custom rules. Give it a try, share your thoughts, and let's collectively enhance the world of JSON parsing for API development.

[Feedback and Contributions Welcome!](https://github.com/techatpark/sjson/issues)

