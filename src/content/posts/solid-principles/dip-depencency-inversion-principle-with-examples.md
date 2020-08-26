+++
date = 2020-08-22T14:38:17Z
description = "Description of what the Dependency Inversion Principle is and examples of its usage"
hero = "/uploads/default-hero.jpg"
title = "DIP - Depencency Inversion Principle (with examples)"
[author]
avatar = "/uploads/default-avatar.png"
name = "Nino Sirchia"

+++
The Interface Segretation is a principle postulated by Robert Martin among the **SOLID** Principles for Object Oriented software development.

**SOLID** is a mnemonic achronym that stands for:

* **S**ingle Responsibiliy (SRP)
* **O**pen closed (OCP)
* **L**iskov Substitution (LSP)
* **I**nterface Segregation (ISP)
* **D**ependency Inversion (DIP)

This 5 principles must guide every software developer in wrinting his code. In this article I'll focus on the last one.

This is an article of the SOLID Principles serie. Checkout the other articles here:

* [Single Responsibiliy (SRP)](/posts/solid-principles/single-responsibility-principle)
* [Open/Closed (OCP)](/posts/solid-principles/open-closed-principle)
* [Liskov Substitution (LSP)](/posts/solid-principles/liskov-substitution-principle)
* [Interface Segregation (ISP)](/posts/solid-principles/interface-segregation-principle)

## Dependency Inversion Principle

The dependecy inversion principle says that

> High-level modules should not depend on low-level modules. Both should depend on abstractions (e.g. interfaces).
>
> Abstractions should not depend on details. Details (concrete implementations) should depend on abstractions.

## About the creator

[**Robert Martin**](https://en.wikipedia.org/wiki/Robert_C._Martin), aka _"Uncle Bob"_ is a coder since 1970 and he's now a world-wide-appreciated software architect, ICT expert and clean code evangelist. Together with Martin Fowler, Ken Shwaber and other forteen people, he was also one of the creator of the [Agile Manifesto](https://agilemanifesto.org/) that is now a guideline for many development team all around the world.

## References

* Agile Software Development: Principles, Patterns and Practices - Robert C. Martin
* The Clean Coder: A Code of Conduct for Professional Programmers - Robert C. Martin
* Clean architecture - Robert C. Martin