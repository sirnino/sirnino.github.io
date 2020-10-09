+++
date = 2020-08-18T18:46:00Z
description = "Description of what the Interface Segregation Principle is and examples of usage"
hero = "/uploads/default-hero.jpg"
title = "ISP - Interface Segregation Principle (with examples)"
[author]
avatar = ""
name = "Nino Sirchia"

+++
The Interface Segretation is a principle postulated by Robert Martin among the **SOLID** Principles
for Object Oriented software development.

**SOLID** is a mnemonic achronym that stands for:

* **S**ingle Responsibiliy (SRP)
* **O**pen closed (OCP)
* **L**iskov Substitution (LSP)
* **I**nterface Segregation (ISP)
* **D**ependency Inversion (DIP)

This 5 principles must guide every software developer in wrinting his code. In this article I'll focus on the fourth one.

This is an article of the SOLID Principles serie. Checkout the other articles here:

* [Single Responsibility (SRP)](/posts/solid-principles/single-responsibility-principle)
* [Open closed (OCP)](/posts/solid-principles/open-closed-principle)
* [Interface Segregation (LSP)](/posts/solid-principles/liskov-substitution-principle)
* [Dependency Inversion (DIP)](/posts/solid-principles/dip-depencency-inversion-principle-with-examples)

## The Interface Segregation Principle

The Interface Segregation Principle says that

> _"No client should be forced to depend on methods it does not use"_

The principle means that each class should expose the minimum set of methods that are necessary for it's purposes.

To make it more clear, let's translate it in code.
Imagine that you're designing a system that must be integrated with three different clients, written by three different development teams:

* Client 1 that uses only an operation named Op1
* Client 2 that uses only an operation named Op2
* Client 3 that uses only an operation named Op3

You could implement all three operations as follow:

```java
     public class Ops{
	 
		public void op1(){
			//Do Op1 stuff
		}
		
		public void op2(){
			//Do Op2 stuff
		}
		
		public void op3(){
			//Do Op3 stuff
		}
	 }
	 
	 public class Client1{
		private Ops ops = new Ops();
		
		//Use of only op1 from ops
	 }
	 
	 public class Client2{
		private Ops ops = new Ops();
		
		//Use of only op2 from ops
	 }
	 
	 public class Client3{
		private Ops ops = new Ops();
		
		//Use of only op3 from ops
	 }
```

But this is not an ISP-compliant approach because all the three clients would have the chance to invoke both the op1, op2 and op3 method.
The idea behind the ISP is that, when a Client has access to a class should see only the methods he is interested in.

This goal can be accomplished by exploiting the Java Interfaces.

The ISP-compliant code is:

```java
     public interface Client1Ops{
		public void op1();
	 }
	 
	 public interface Client2Ops{
		public void op2();
	 }
	 
	 public interface Client3Ops{
		public void op3();
	 }
	 
	 
	 public class Ops implements Client1Ops, Client2Ops, Client3Ops{
	 
		public void op1(){
			//Do Op1 stuff
		}
		
		public void op2(){
			//Do Op2 stuff
		}
		
		public void op3(){
			//Do Op3 stuff
		}
	 }
	 
```

In this case the clients will use the ops as follow:

```java
	public class Client1{
		private Client1Ops ops = new Ops();
		
		//Use of op1 from ops
	 }
	 
	 public class Client2{
		private Client2Ops ops = new Ops();
		
		//Use of op2 from ops
	 }
	 
	 public class Client3{
		private Client3Ops ops = new Ops();
		
		//Use of op3 from ops
	 }
```

In this case, even if the Ops class implements all the methods, each client will interact with such implementation through the interface
that will make visible only the methods the client is interested in.

## About the creators

[**Robert Martin**](https://en.wikipedia.org/wiki/Robert_C._Martin), aka _"Uncle Bob"_ is a coder since 1970 and he's now a world-wide-appreciated software architect, ICT expert and clean code evangelist.
Together with Martin Fowler, Ken Shwaber and other forteen people, he was also one of the creator of the [Agile Manifesto](https://agilemanifesto.org/) that is now a guideline for many development team all around the world.

## References

* Agile Software Development: Principles, Patterns and Practices - Robert C. Martin
* The Clean Coder: A Code of Conduct for Professional Programmers - Robert C. Martin
* Clean architecture - Robert C. Martin