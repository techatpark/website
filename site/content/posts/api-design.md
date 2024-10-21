---
title: "API Design: The Art of Programming"
weight: 9
authors:
  - sathishk
  - hari-nikesh-r
---

APIs are the backbone of modern software, and developers create them daily. Yet, many treat API creation as a task to complete rather than an art to refine. Often, we design interfaces to serve an immediate purpose without thinking deeply about their structure. But API design is more than a technical process—it’s a craft requiring thoughtfulness, intuition, and an eye for elegance. While techniques can be taught, true API design involves creating something that is functional, user-friendly, and maintainable in the long run. 

> **API Design** is the process of creating APIs that not only achieve the task but do so in a way that's simple, easy to understand, and optimized. A well-designed API should make life easier for the developer, the user, and the system. In short, good API design is clear, efficient, and user-friendly.

### A Simple Example in Modern Java

In modern Java, convenience methods like `List.of()` simplify working with collections. Previously, creating a list of two string values required:

```java
import java.util.List;
import java.util.ArrayList;

List<String> values = new ArrayList<>();
values.add("Sathish");
values.add("Hari Nikilesh");
```

Now, this can be done with:

```java
import java.util.List;
List<String> values = List.of("Sathish", "Hari Nikilesh");
```

Is the improvement just fewer lines of code? Not quite.

### Capturing Developer Intent

Good API design makes everyone happy—even your computer. When a developer wants to create a list of two strings, the intent wasn’t fully clear in the original API:

```java
List<String> values = new ArrayList<>();
```

The improved version, `List.of()`, captures this intent precisely:

```java
List.of("Sathish", "Hari Nikilesh")
```

This communicates clearly to the API:

1. You need a `List`.
2. It holds `String` values.
3. It contains exactly two elements.

Here’s how Java internally implements `List.of()`:

```java
static <E> List<E> of(E e1, E e2) {
    return new ImmutableCollections.List12<>(e1, e2);
}

List12(E e0, E e1) {
    this.e0 = Objects.requireNonNull(e0);
    this.e1 = Objects.requireNonNull(e1);
}
```

Instead of using arrays, Java optimizes this with individual elements, creating an immutable, memory-efficient list. It makes the developer happy by capturing intent, reduces code for the consumer, and is more efficient for the system.

API design truly is **The Art of Programming**.!