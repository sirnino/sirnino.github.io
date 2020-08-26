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

Let's do an example to better explain it.

Imagine to design a software with the following class diagram:

![](/assets/images/dip-1.png)

The main App uses directly the ExcelExporter class as follows:

    public class App {
    	private ExcelExporter exporter = new ExcelExporter();
        
        public File export(){
        	return exporter.toFile();
        }
    }

Here we have that the high-level module (App class) depends on low-level component (ExcelExporter class).

The problem is that if we need to produce a different File (e.g. a PDF file instead of an Excel) we have to modify the code of the App as follows:

    public class App {
    	private PDFExporter exporter = new PDFExporter();
        
        public File export(){ 
        	return exporter.toFile();  
        } 
    }

As we've already seen, this is not compliant with the Open-Closed Principle and is hard to maintain.

A better design adopts the Dependency Inversion as follows:

![](/assets/images/dip-2.png)

Here the inversion of the dependency is quite visible: both the ExcelExporter and PDFExporter depends on the abstract module _Exporter_.

The corresponding code is:

    public interface Exporter {
    	public File toFile();
    }
    
    public class ExcelExporter implements Exporter {
    	public File toFile(){
        	//Arrange contents in Excel File
        }
    }
    
    public class PDFExporter implements Exporter {
    	public File toFile(){
        	//Arrange contents in PDF File
        }
    }
    
    public class App{
    	private Exporter exporter;
        
        public App(Exporter exporter){
        	this.exporter = exporter;
        }
        
        public File export(){ 
        	return exporter.toFile();  
        } 
    }

The specific exporter implementation can be provided through the constructor as follows:

    App app = new App(new ExcelExporter());

or

    App app = new App(new PDFExporter());

leaving the App class agnostic about the specific implementation used at runtime.

The usage of the constructor for the injection of the dependency is just an example, other approaches can be adopted; for example the Factory class or Java Reflection or both of them.

### Dependency injection through Factory class

    public class ExporterFactory{
    	public static Exporter getExporter(){
        	return new ExcelExporter();
        }
    }
    
    public class App{
    	private Exporter exporter;
        
        public App(){
        	this.exporter = ExporterFactory.getExporter();
        }
        
        public File export(){ 
        	return exporter.toFile();  
        } 
    }

### Dependency injection through Java Reflection

This approach uses a property file containing the complete classname of the implementation to use.

    exporter.impl.class=io.github.sirnino.ExcelExporter

Through Java reflection the developer can dynamically instantiate a 

    public class App{
    	private Exporter exporter;
        
        public App(){
        	String classname = Property.get("exporter.impl.class");
            Class<Exporter> clazz = Class.getInstanceFor(classname);
        	this.exporter = clazz.getInstance();
        }
        
        public File export(){ 
        	return exporter.toFile();  
        } 
    
    }

### Dependency Injection through Factory class and Java Reflection

A more SRP-compliant approach is the following:

    exporter.impl.class=io.github.sirnino.ExcelExporter

    public class ExporterFactory{
    	public static Exporter getExporter(){
        	String classname = Property.get("exporter.impl.class");
            Class<Exporter> clazz = Class.getInstanceFor(classname);
        	this.exporter = clazz.getInstance();
        }
    }
    
    public class App{
    	private Exporter exporter;
        
        public App(){
        	this.exporter = ExporterFactory.getExporter();
        }
        
        public File export(){ 
        	return exporter.toFile();  
        } 
    }

Here the business logic for the object allocation is delegated to the Factory class that uses the Java Reflection for obtaining the reference to which class it must create an instance of.

## About the creator

[**Robert Martin**](https://en.wikipedia.org/wiki/Robert_C._Martin), aka _"Uncle Bob"_ is a coder since 1970 and he's now a world-wide-appreciated software architect, ICT expert and clean code evangelist. Together with Martin Fowler, Ken Shwaber and other forteen people, he was also one of the creator of the [Agile Manifesto](https://agilemanifesto.org/) that is now a guideline for many development team all around the world.

## References

* Agile Software Development: Principles, Patterns and Practices - Robert C. Martin
* The Clean Coder: A Code of Conduct for Professional Programmers - Robert C. Martin
* Clean architecture - Robert C. Martin