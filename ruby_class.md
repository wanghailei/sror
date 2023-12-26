# Class

Classes are, at heart, a way to organise objects and methods.\
==% 與其說 organise，毋寧說 define 或 design，可以說是「藍圖」。 20231117%==

Defining a class lets you group behaviours (methods) into convenient bundles, so that you can quickly create many objects that behave essentially the same way.

Everything you handle in Ruby is either an object or a construct that evaluates to an object, and every object is an instance of some class.

When you use the dot notation on a class, you send a message to the class. Classes can respond to messages.



Ruby is about objects.

Objects are instances of classes.

Classes are objects.

`Object` is a built-in Ruby class.

Classes are named with constants.

==% 定義一個 Class，就像「開模」來製造一個銅盤一樣。Class就是模具。20230624 %==



***

### Learned from Xavier Noria&#x20;

==The `class` and `module` keywords store classes and modules in constants.==

In Ruby, when you define a class or a module using the `class` or `module` keywords, they are indeed stored as constants. This is a unique aspect of Ruby's object model. For example, when you define `class MyClass; end`, `MyClass` is a constant that references the class object.

==Constants belong to classes and modules.==

Constants in Ruby are scoped within classes and modules. They are not global in the same sense as in some other languages. This means you can have different constants with the same name in different scopes without conflict. For instance, you could have `class A; MY_CONST = 1; end` and `class B; MY_CONST = 2; end` without any conflict between `A::MY_CONST` and `B::MY_CONST`.

==Top-level constants belong to `Object.==

In Ruby, top-level constants (those defined outside of any class or module) are treated as if they belong to the `Object` class. This is because `Object` is the default object context of Ruby at the top level. This means that any constant defined at the top-level is accessible from anywhere in the program, as all classes in Ruby are descendants of `Object`.

`Module#autoload` allows you to load constants on demand.



***

## Singleton Class

In Ruby, ==each object has its own singleton class== (also known as a metaclass or eigenclass). \
==The singleton class is a subclass of the object's class.== This singleton class is automatically created by Ruby the first time you define a singleton method on the object.&#x20;

The singleton class is a core aspect of Ruby's object-oriented design, which emphasizes flexibility and expressiveness. Here are some key reasons why singleton classes are used:

1. **Implementing Class Methods**: ==In Ruby, class methods are actually instance methods of the class's singleton class.== This is because classes themselves are also objects in Ruby, so each class has its own singleton class where its class methods are stored.
2. **Individual Object Customisation**:  ==Singleton classes allow you to add methods to an individual object rather than to an entire class of objects.== Without singleton class, the only way would be to modify its class. However, modifying a class affects all instances of that class, which can lead to unexpected side effects. \
   Especially, when you want to add functionality to instances of core classes (like String, Array, etc.) without affecting all instances, singleton classes are the way to go. This is often used in Ruby on Rails and other frameworks to extend the capabilities of standard objects on a per-instance basis.\
   &#x20;==% Why don't use mixin? 20231223 %==
3. **Supporting Metaprogramming**: Ruby's metaprogramming capabilities are largely facilitated by singleton classes. They allow dynamic addition of methods at runtime, making Ruby a very flexible and powerful language for metaprogramming.
4. **Method Look-Up Consistency**: Ruby maintains a consistent method look-up path. ==When you call a method on an object, Ruby first looks in the object's singleton class before looking in the object's actual class and its ancestors.==&#x20;



***

## Methods

Methods defined inside a class and intended for use by all instances of the class, are called instance methods.

Methods that you define for one particular object are called singleton methods.

A class method belongs to the class itself.

==%. 有三種 methods：== 

==Class methods：這是 class 給自己（工廠）用的；== 

==Instance methods：這是 class 安裝進生產出來的 instance（object）上的；還有== 

==Singleton methods：這是某一個 instance 或 object 在被生成後，自己搞來用的。== 

==20231223 %==

### What Are Class Methods For?

Why create a class method rather than the more usual instance method? 
There are two main reasons: First, a class method can ==be used as a “ready-to-run function” without having to go to the bother of creating an object just to use it==, and second, ==it can be used on those occasions when you need to run a method before an object has been created==.





