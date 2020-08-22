+++
date = 2020-08-12T16:33:00Z
description = "Description of what the Single Responsibiliy Principle is and examples of usage"
hero = "/uploads/default-hero.jpg"
title = "SRP - Single Responsibiliy Principle (with examples)"
[author]
avatar = ""
name = "Nino Sirchia"

+++
The Single Responsibiliy is one of the **SOLID** Principles postulated by Robert Martin.

**SOLID** is a mnemonic achronym that stands for:

* **S**ingle Responsibiliy (SRP)
* **O**pen closed (OCP)
* **L**iskov Substitution (LSP)
* **I**nterface Segregation (ISP)
* **D**ependency Inversion (DIP)

This 5 principles must guide every software developer in wrinting his code. In this article I'll focus on the first one.

This is an article of the SOLID Principles serie. Checkout the other articles here:

* [Open closed (OCP)](/posts/solid-principles/interface-segregation-principle)
* [Liskov Substitution (LSP)](/posts/solid-principles/liskov-substitution-principle)
* [Interface Segregation (ISP)](/posts/solid-principles/interface-segregation-principle)
* [Dependency Inversion (DIP)](/posts/solid-principles/dip-depencency-inversion-principle-with-examples)

## The Single Responsibiliy Principle

The Single Responsibiliy Principle says that

> _"A module should have one and only one reason to change"_

This principle means that a module (e.g. a Java Class) should change only for one specific reason. As it is, this principle is interpretaion prone, so we can also read it as:

> _"Each module should be intended to do only one thing"_

And also:

> _"If a change request come, only one module should be affected"_

Imagine that you're coding a system that has three actors:

* The Chief Financial Officer (CFO) that uses the system to calculate the pay of each employee;
* The Chief Operation Officer (COO) that uses the system to report the working hours of each employee;
* The Chief Technology Officer (CTO) that uses the system to save the monthly data in order to emit the paycheck.

What if you code a single class that is in charge for both calculate the pay, report the working hours and save the monthly data?

```java
     public class Employee{
		//All the private fields here
		
		public float calcPay(){
			...
		}
		
		public void reportHours(float hours){
			...
		}
		
		public void save(){
			...
		}
	 }
```

You' would have the following situation

![](/assets/images/srp-1.png)

Here, we would have that every re-compilation of the Employee class due, for example, to a revision to the calcPay method will involve also a recompilation of the reportHours method.
This is something deprecable because, basing on the revision is done, the other methods could reach an inconsistent state, causing a regression.

A SRP compliant code is the following:

```java
	  public class PayCalculator{
		  //pay calculation specific private fields 
		
		  public float calcPay(){
			...
		  } 
	  }
	  
	  public class HourReporter{
		  //hours reporting specific private fields 
		
		  public void reportHours(float hours){
			...
		  } 
	  }
	  
	  public class DataSaver{
		  //data saving specific private fields 
		
		  public void save(){
			...
		  } 
	  }
```

![](/assets/images/srp-2.png)

Where each actor communicate with a component designed for his own specific purposes.

If a revision of the calcPay method is requested, there is no way to affect the HourReporter or DataSaver modules because, now, they are totally decoupled.

Other benefits of this approach are:

* **Testability**: Each module is easily testable without interferences;
* **Maintainability**: The modules are more lightweight and have also a lower cognitive complexity then a big monolithic module.

## About the creator

The SOLID principles were postulated by Robert Martin nei primi anni 2000.
[**Robert Martin**](https://en.wikipedia.org/wiki/Robert_C._Martin), aka _"Uncle Bob"_ is a coder since 1970 and he's now a world-wide-appreciated software architect, ICT expert and clean code evangelist.
Together with Martin Fowler, Ken Shwaber and other forteen people, he was also one of the creator of the [Agile Manifesto](https://agilemanifesto.org/) that is now a guideline for many development team all around the world.

## References

* Agile Software Development: Principles, Patterns and Practices - Robert C. Martin
* The Clean Coder: A Code of Conduct for Professional Programmers - Robert C. Martin
* Clean architecture - Robert C. Martin