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

# 4. Observer (Behavioral)

# 5. Facade (Architectural)

# 6. Lazy Loading (Performance)