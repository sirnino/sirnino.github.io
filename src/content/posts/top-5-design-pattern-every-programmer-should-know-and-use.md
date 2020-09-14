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

A design pattern is an abstraction of the best solution to a frequent problem in software development.

# Why to use a design pattern?

If a developer faces a problem, the best idea he could have is to use a well-known and tested solution, without re-inventing the wheel.

Using a design pattern ensures that side effects won't happen during the development process and, also, that the problem will be solved with the best approach possible.

# 1. Singleton

The Singleton pattern is a creational design pattern that allows to make sure that only one instance of a certain class is created during the software lifecycle.

A class that must be a Singleton has 3 main requirements:

* must have a **private constructor**
* must have a private static field that is an **instance of itself**
* must have a **getInstance** static method that, in a thread safe way, provides the unique instance

    package io.github.sirnino;
    
    public class MySingleton {
    	
    	private static MySingleton instance;
    	
    	private MySingleton() {
    		//Do your construction stuff
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

# 2. Factory (Creational)

# 3. Strategy (Behavioral)

# 4. Observer (Behavioral)

# 5. Facade (Architectural)

# 6. Lazy Loading (Performance)