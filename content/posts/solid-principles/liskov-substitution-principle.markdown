+++
date = 2020-08-14T18:10:00Z
description = "Description of what the Liskov Substitution Principle is and examples of usage"
hero = "/uploads/default-hero.jpg"
title = "LSP - Liskov Substitution Principle (with examples)"
[author]
avatar = ""
name = "Nino Sirchia"

+++
The Liskov Substitution is a principle postulated by Barbara Liskov and included by Robert Martin among the **SOLID** Principles
for Object Oriented software development.

**SOLID** is a mnemonic achronym that stands for:

* **S**ingle Responsibiliy (SRP)
* **O**pen closed (OCP)
* **L**iskov Substitution (LSP)
* **I**nterface Segregation (ISP)
* **D**ependency Inversion (DIP)

This 5 principles must guide every software developer in wrinting his code. In this article I'll focus on the third one.

This is an article of the SOLID Principles serie. Checkout the other articles here:

* [Single Responsibiliy (SRP)](/programming/solid/2020/08/12/solid-srp.html)
* [Open/Closed (OCP)](/programming/solid/2020/08/13/solid-ocp.html)
* [Interface Segregation (ISP)](/programming/solid/2020/08/18/solid-isp.html)
* [Dependency Inversion (DIP)](/posts/solid-principles/dip-depencency-inversion-principle-with-examples)

## The Liskov Substitution Principle

The Liskov Substitution Principle says that

> _"In a computer program P, if S is a subtype of T, then objects of type T may be replaced with objects of type S (i.e., objects of type S may substitute objects of type T) without altering any of the desirable properties of P (correctness, task performed, etc.)"_

To make it more clear, let's translate it in code:

```java
     public class P{
	 
		private T myField = new T();
	 
	 }
	 
	 public class T{
	 
		//T implementation
	 
	 }
	 
	 public class S extends T{
	 
		//S implementation
	 
	 }
```

The LSP states that if you change the Program P as follows:

```java
     public class P{
	 
		private T myField = new S();
	 
	 }
```

The program should still work as expected.

Now let's move to a more concrete example and let's look how is LSP violation simple.

Let's pretend having the class `Message` used by the the class `Program` as follows:

```java
     public class Message{
	 
		private String title;
		private String text;
		
		public void setTitle(String t){
			this.title = t;
		}
		
		public void setText(String txt){
			this.text = txt;
		}
		
		public String getText(){
			return this.text;
		}
		
		public String getTitle(){
			return this.title;
		}
	 }
	 
	 public class Program{
	 
		public static void main(String[] args){
			Program p = new Program();
			
			Message m = new Message();
			m.setTitle("Message Title");
			m.setText("Hello World");
			
			saveMessage(m);
			
		}
		
		public void saveMessage(Message m){
			String stringToSave = "====\n" + m.getTitle() + "\n" + m.getText() + "\n====\n";
			
			//Save on disk code
			
		}
		
	 }
```

and now imagine there's a `ChatMessage` class that is a subtype of `Message`

```java
     public class ChatMessage extends Message{
	 
		private String recipient;
		
		public void setRecipient(String rcpt){
			this.recipient = rcpt;
		}
		
		public String getRecipient(){
			return this.recipient;
		}
	}
```

Can we substitute the `Message` object in `Program` with an `ChatMessage` object?

```java
     public class Program{
	 
		public static void main(String[] args){
			Program p = new Program();
			
			ChatMessage e = new ChatMessage();
			e.setTitle("Message Title");
			e.setText("Hello World");
			e.setRecipient("sirnino");
			
			saveMessage(e);
			
			Message m = new Message();
			m.setTitle("Message Title");
			m.setText("Hello World");
			
			saveMessage(m);
		}
		
		public void saveMessage(Message m){
			String stringToSave = "====\n" + m.getTitle() + "\n" + m.getText() + "\n====\n";
			
			//Save on disk code
		}
```

The answer is **no**. Since, as the name states, the goal of the `saveMessage` method is to save a serialization of a message,
with the `ChatMessage` object such a goal cannot be accomplished, since we loose information about the recipient;

In order to obtain such a goal, we should customize the `saveMessage` code to something like:

```java
	public void saveMessage(Message m){
		String stringToSave = "";
		if(m instanceof Message){
			stringToSave += "====\n" + m.getTitle() + "\n" + m.getText() + "\n====\n";
		}
		else if(m instanceof ChatMessage){
			stringToSave += "====\n" + m.getTitle() + "\n" + "To: " + m.getRecipient() + "\n" + m.getText() + "\n====\n";
		}
			
		//Save on disk code
	}
```

Ok but what if tomorrow a new subtype of `Message` comes? Let's imagine an `Email` class:

```java
     public class Email extends Message{
	 
		private List<String> to;
		
		private List<String> cc;
		
		private List<String> ccn;
		
		//All getters and setters
	}
```

another if statement should be added to the `saveMessage` method in order to deal with this new kind of Object, and so on and so forth for any other
new extension of `Message`. This is absolutely poor code, hard to read, hard to mantain and error prone.

What the LSP recommend, between the lines, is to arrange a well defined extension hierarchy that makes the code robust, easy to read and mantain.

In this case we could design a hierarchy as the following:

![](/assets/images/lsp-1.png)

This will allow us to design specific and consistent savers for each message type from the more general to the more detailed.

## About the creators

[**Barbara Liskov**](https://en.wikipedia.org/wiki/Barbara_Liskov) is an american computer scientist and Institute Professor at Boston MIT.
In 2008 she won the Turing award for her contribution in the Object Oriented Programming principle definition.

[**Robert Martin**](https://en.wikipedia.org/wiki/Robert_C._Martin), aka _"Uncle Bob"_ is a coder since 1970 and he's now a world-wide-appreciated software architect, ICT expert and clean code evangelist.
Together with Martin Fowler, Ken Shwaber and other forteen people, he was also one of the creator of the [Agile Manifesto](https://agilemanifesto.org/) that is now a guideline for many development team all around the world.

## References

* Agile Software Development: Principles, Patterns and Practices - Robert C. Martin
* The Clean Coder: A Code of Conduct for Professional Programmers - Robert C. Martin
* Clean architecture - Robert C. Martin

# Need help?

If you're trying to adopt the Liskov Substitution Principle and you're stucked or you just want a review, you can contact me on fiverr to check your code together.
- For java code click [here](https://www.fiverr.com/share/9zKyk0)
- For javascript code click [here](https://www.fiverr.com/share/pjDq5y)