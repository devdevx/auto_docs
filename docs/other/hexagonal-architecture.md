# Hexagonal architecture

## Introduction

## Kotlin

```
.
+-- root.package
|   +-- App.kt
|   +-- commons
|   +-- config
|   +-- app
|       +-- inbound
|       +-- outbound
|       +-- domain
|           +-- models
|           +-- services
|           +-- providers
|           +-- repositories
```

Mapping functions are declared with extension functions

```kotlin
fun Domain.toResource() = Resource(
	resourceValue = this.domainValue,
)
```

Use `val` in all attributes and the method `copy()` to perform mutations

```kotlin
data class Counter(val value: Int)
val newCounter = counter.copy(value = 0)
```





https://www.baeldung.com/hexagonal-architecture-ddd-spring

