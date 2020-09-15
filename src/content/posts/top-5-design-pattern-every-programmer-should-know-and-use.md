+++
date = 2020-09-12T16:51:47Z
description = ""
draft = true
hero = "/uploads/default-hero.jpg"
title = "Top 5 design pattern every Programmer should know (and use)"
[author]
avatar = "/uploads/default-avatar.png"
name = "Nino Sirchia"

+++
# TLDR

Following a design pattern is the best way possible you have to solve a problem without undesired side effects.

There are a lot of design patterns for many different purposes. But the top 5, in my opinion, is the following one:

1. Singleton (Creational Pattern)
2. Factory (Creational Pattern)
3. Strategy (Behavioral Pattern)
4. Observer (Behavioral Pattern)
5. Facade (Architectural Pattern)
6. Lazy Loading (Performance Pattern)

# What is a design pattern?

Every developer, sooner or later, is faced with frequent problems for which someone else, on the basis of various experiences, has defined a solution universally recognized as "the best one".

**A design pattern is an abstraction of the best solution to a frequent problem in software development**.

# Why to use a design pattern?

If a developer faces a problem, the best idea he could have is to use a well-known and tested solution, without re-inventing the wheel.

Using a design pattern ensures that side effects won't happen during the development process and, also, that the problem will be solved with the best approach possible.

# 1. Singleton

The Singleton pattern is a creational design pattern that allows to make sure that only one instance of a certain class is created during the software lifecycle. This is required for example for database connections, http clients, etc...

In order to be a good Singleton, a class must follow 3 main requirements:

* must have a **private constructor**
* must have a private static field that is an **instance of itself**
* must have a **getInstance** static method that, in a thread safe way, provides the unique instance

The following is an example of Singleton class.

    public class MySingleton {
    	
    	private static MySingleton instance;
    	
    	private MySingleton() {
            //Do your construction stuff. Nothing in this example
    	}
    	
    	public static MySingleton getInstance() {
    		MySingleton localRef = instance;
            if (localRef == null) {
                synchronized (MySingleton.class) {
                    localRef = instance;
                    if (localRef == null) {
                    	instance = localRef = new MySingleton();
                    }
                }
            }
            return localRef;
    	}
    	
    	public void dump() {
    		System.out.println(this);
    	}
    }

Here is also the code for the main:

    	public static void main(String[] args) {
    		MySingleton inst1 = MySingleton.getInstance();
    		inst1.dump();
    		
    		MySingleton inst2 = MySingleton.getInstance();
    		inst2.dump();
            
            System.out.println(inst1.equals(inst2));
    	}

The output, as expected, is something like:

    io.github.sirnino.MySingleton@7852e922
    io.github.sirnino.MySingleton@7852e922
    true

# 2. Factory

The Factory pattern is a creational design pattern that allows to **encapsulate the object instantiation logic in a single point**: the Factory Class. This ensures to avoid having "new" keyword scattered all around the codebase and to have a more mantainable code.

The keypoints to properly implement such a pattern are:

* a Factory Class that creates the objects
* an enumeration that can be used as keyword to decide which kind of object the Factory should allocate

Here is an example.

    public interface Person {
    	public String getWork();	
    }
    
    public enum PersonType {
    	STUDENT,
    	EMPLOYEE;
    }
    
    public class Employee implements Person{
    
    	private static final String DESCRIPTION = "Engineer";
    	
    	@Override
    	public String getWork() {
    		return DESCRIPTION;
    	}
    
    }
    
    public class Student implements Person{
    
    	private static final String DESCRIPTION = "Student";
    	
    	@Override
    	public String getWork() {
    		return DESCRIPTION;
    	}
    
    }

The Factory class could be something like the following:

    public class MyFactory {
    
    	public static Person getPerson(PersonType type) {
    		Person ret;
    		switch(type) {
    			case STUDENT:
    				ret = new Student();
    				break;
    			case EMPLOYEE:
    				ret = new Employee();
    				break;
    			default:
    				throw new RuntimeException("Unknown type "+type);
    		}
    		
    		return ret;
    	}
    
    }

It can be used as follows:

    	public static void main(String[] args) {
    		
    		Person p1 = MyFactory.getPerson(PersonType.STUDENT);
    		System.out.println(p1.getWork());
    		
    		Person p2 = MyFactory.getPerson(PersonType.EMPLOYEE);
    		System.out.println(p2.getWork());
    		
    	}

The Output of this code is the following:

    Student
    Engineer

# 3. Strategy

The Strategy pattern is a behavioral design pattern that allows to **scaffold a certain algorithm and provide the specific implementation at runtime**.

This allows to make the implementation of a algorithms family interchangable.

The keypoints to properly implement such a pattern are:

* an interface that allows to abstract the steps of the algorithm
* a constructor that receives the desired interface implementation

Here is an example:

* an interface that defines the steps of the process

    public interface MyProcess {
    	
    	public void extract();
    	
    	public void transform();
    	
    	public void load();
    
    }
    

* a set of interchangable implementations of the interface

    public class ProcessOne implements MyProcess {
    
    	@Override
    	public void extract() {
    		System.out.println("Get data via HTTP");
    	}
    
    	@Override
    	public void transform() {
    		System.out.println("Convert them in XML");
    	}
    
    	@Override
    	public void load() {
    		System.out.println("Save them into Postgres Database");
    	}
    
    }
    
    public class ProcessTwo implements MyProcess {
    
    	@Override
    	public void extract() {
    		System.out.println("Get data via FTP");
    	}
    
    	@Override
    	public void transform() {
    		System.out.println("Convert them in CSV");
    	}
    
    	@Override
    	public void load() {
    		System.out.println("Save them into MongoDB Database");
    	}
    
    }
    
    public class ProcessThree implements MyProcess {
    
    	@Override
    	public void extract() {
    		System.out.println("Get data from MySQL");
    	}
    
    	@Override
    	public void transform() {
    		System.out.println("Do Nothing");
    	}
    
    	@Override
    	public void load() {
    		System.out.println("Send them via HTTP");
    	}
    
    }

* a processor class that receives in the constructor the interface implementation to use

    public class Processor {
    	
    	private MyProcess proc;
    	
    	public Processor(MyProcess processToExecute) {
    		this.proc = processToExecute;
    	}
    		
    	public void run() {
    		proc.extract();
    		proc.transform();
    		proc.load();
    	}
    
    }

* the main program that uses the processor

    	public static void main(String[] args) {
    		
    		Processor processor1 = new Processor(new ProcessOne());
    		processor1.run();
    		
    		Processor processor2 = new Processor(new ProcessTwo());
    		processor2.run();
    		
    		Processor processor3 = new Processor(new ProcessThree());
    		processor3.run();
    		
    	}

The output of this example is the following:

    Get data via HTTP
    Convert them in XML
    Save them into Postgres Database
    
    Get data via FTP
    Convert them in CSV
    Save them into MongoDB Database
    
    Get data from MySQL
    Do Nothing
    Send them via HTTP

# 4. Observer

The Observer pattern is a behavioral design pattern that allows to **decouple events handling from the main program**.

Imagine having a main program that triggers many events, e.g. data insertion in DB, and the program must be **reactive** to these events. The observer is the perfect pattern for this use cases

The keypoints to properly implement such a pattern are:

* an interface that define a common signature for all the observers
* a class, acting as event emitter, that loops through all the observers in order to notify them

Here is an example:

* the Observer interface defines the signature for the _react_ method

    public interface Observer {
    	
    	public void react();
    
    }

* a set of classes that implements such an interface

    public class Notifier implements Observer {
    
    	@Override
    	public void react() {
    		System.out.println("Notify 3rd party application via HTTP");
    	}
    
    }
    
    public class Logger implements Observer {
    
    	@Override
    	public void react() {
    		System.out.println("Log event on central log server");
    	}
    
    }
    
    public class Validator implements Observer {
    
    	@Override
    	public void react() {
    		System.out.println("Validate the submitted data");
    	}
    
    }

* a class acting as event emitter

    import java.util.ArrayList;
    import java.util.List;
    
    public class DataHandler {
    	
    	private List<Observer> observers = new ArrayList<>();
    	
    	public void addObserver(Observer obs) {
    	    observers.add(obs);
    	}
    
    	public void removeObserver(Observer obs) {
    		observers.remove(obs);
    	}
    	
    	public void saveData(int data) {
    		
    		System.out.println("Data "+data+" saved correctly");
    		
    		notifyObservers();
    	}
    	
    	public void notifyObservers() {
    		observers.forEach(Observer::react);
    	}
    
    }

* the main program has only to register the observers and trigger the event

    	public static void main(String[] args) {
    		DataHandler dh = new DataHandler();
    		
    		dh.addObserver(new Validator());
    		dh.addObserver(new Notifier());
    		dh.addObserver(new Logger());
    		
    		dh.saveData(1);
    		System.out.println("=====");
    		
    		dh.saveData(2);
    		System.out.println("=====");
    		
    		dh.saveData(3);
    		System.out.println("=====");
    
    	}

# 5. Facade (Architectural)

# 6. Lazy Loading (Performance)