---
title: "C# Yield"
date: '2025-10-27T09:06:50+08:00'
tags:
  - C#
AI-generated note: true
---

## 🧩 Intent

The `yield` keyword simplifies the creation of iterators by allowing a method to produce a sequence of values lazily, one at a time, without building a collection in memory.

---

## 💡 Description

- `yield return <value>`: Produces a value to the enumerator and pauses execution until the next iteration.
    
- `yield break`: Terminates the iteration early.
    

When a method uses `yield`, the C# compiler automatically generates a **state machine** that implements `IEnumerable` and `IEnumerator`. This allows the method to pause and resume execution seamlessly across iterations.

---

## ⚙️ Example

```csharp
IEnumerable<int> GetNumbers()
{
    yield return 1;
    yield return 2;
    yield return 3;
}

foreach (var n in GetNumbers())
{
    Console.WriteLine(n);
}
```

**Output:**

```bash
1
2
3
```

---

## 🚫 Early Termination Example

```csharp
IEnumerable<int> GetEvenNumbers(int max)
{
    for (int i = 0; i <= max; i++)
    {
        if (i % 2 != 0) continue;
        if (i > 10) yield break;
        yield return i;
    }
}
```

This function stops producing values once `i > 10`.

---

## 🧠 Use Cases

- Generating sequences on demand (lazy evaluation)
    
- Custom iteration over data structures
    
- Streaming or paging large data sets
    
- Simplifying iterator logic without manually implementing `IEnumerable`
    

---

## ⚖️ Comparison

|Without `yield`|With `yield`|
|---|---|
|Must allocate a collection (e.g., `List<T>`)|No extra collection needed|
|Returns only after full computation|Returns as soon as first value is ready|
|Higher memory usage|Lower memory footprint|

---

## 🧭 Summary

`yield` turns complex iterator logic into simple, readable code. It provides a **pause-and-resume** mechanism for methods, improving performance and readability in iterative scenarios.

---

## 📚 References

- [Microsoft Docs - yield (C# Reference)](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/yield)
    
- [C# Iterators Overview](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/iterators)