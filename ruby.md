# Ruby lang

This philosophy is often summarized as: "Ruby is designed to make programmers happy."

Human-Centric Design: Matz designed Ruby with an emphasis on the needs of humans rather than computers, which makes it intuitive and easy to read. It emphasises natural language elements, significant whitespace, and common idioms, so Ruby code often reads like English sentences.

Flexible: Ruby is designed to be flexible to allow programmers to have multiple ways to do the same thing. This gives you the freedom to write code that best suits your thinking process.

Consistent: In Ruby, everything is an object, and all of those objects have methods. This consistent, object-oriented approach makes Ruby code easy to understand and predict. Even basic data types like integers are objects with methods.

Metaprogramming: Ruby has robust metaprogramming capabilities. This means you can write code that generates other code, making Ruby very powerful and flexible.

Blocks, Procs, and Lambdas: Ruby features first-class support for "blocks" of code and makes it easy to pass these blocks around your program. This feature is heavily used in Ruby for handling everything from basic iteration to customising how complex objects behave.



***

### Concepts

object 形體

class 形組

type 形式

attribute 形態

method 形變

OO 以「形體」為主導的模式。

### Metaphors

符號「`.`」其實相當於英文裡的「'」或者中文裡的「的」。

一個 Function 就像一台小機器，被調用（call）時，就會進行「來料加工」，然後根據「指定規格」（-> type）返回（return）一個結果。

那麼，我想，一個 Struct 或一個 Class 就像一個個的工廠🏭。

Variable 或 Constant 就是些容器/載具，而且可能是透明材質的，用來裝東西（value）。

let 類型的容器，是放進去就再也更改不了的，叫做「非換裝容器」；而 var 類型的容器，是放進去的東西以後還可以換裝別的，叫做「可換裝容器」。

每一種容器，只能裝一種固定「型態」的東西，例如長的、寬的、球的、扁的、水的、氣的等等。

被大括號 `{}` 包起來的叫做 code block「碼塊」，裡面是實際上會執行的內容。

### Type 形態 / 形式 / 模樣 / 形狀

<mark style="background-color:red;">我認為 type 翻譯成「形態」/「型態」比較合適，甚至叫「形狀」或「模樣」都很好。因為一個 type 確實表現的是一段代碼的構成樣式、形狀、構造，如果這種樣式經常被看到，就可以抽象出來，並起一個名字，也就是稱之為「某型代碼」或「某種形態代碼」。這跟虎形、鶴形；可愛型、性感型，其實是一個道理。</mark>

<mark style="background-color:red;">形，外形、姿態、容貌、樣式等意，例如：形勢、形色、形式等。型，器物的模樣，引申為某種標準，型式、典範、態度、風格之意。例如：模型、典型。二字意思相近，有字典謂兩字相通。所以，凡與外貌有關的，用「形」字；凡人工鑄造出來的，或引申事物表現的格調，用「型」字。</mark>

<mark style="background-color:red;">英文的「形」為shape；英文的「型」為type、style。</mark>

In any programming language there are two main categories of types: primitive and composite. Primitive types are atomic, i.e., they are not formed by the combination of other types. 基本的型態Composite types are made of other types, either primitive or composite. 複合的型態

A data type is the type of data (value) a variable or constant can store in it.

Most programming languages deal with typed values, i.e., integers, booleans, vehicles, etc. There are however, programming languages that have no types at all. BCPL has only one data type, a word. Different operations treat each word as a different type.

A type is, in essence, a set of values. Some of these sets have a finite number of elements, while others are infinite.

For instance, the boolean data type is a set with two elements: true and false; however, the string data type is a set with an infinite number of elements.

Not every operation can be applied on every data type.

Types exist so that developers can represent entities from the real world in their programs. However, types are not the entities that they represent.

Types prevent the program from entering into undefined states.

Types are a form of documentation that the compiler can check.

Types classify programming languages along three most important dimensions: Statically vs Dynamically typed; Strongly vs Weakly typed; Structurally vs Nominally typed.

### Value Types

A value type is a type whose value is copied when it’s assigned to a variable or constant, or when it’s passed to a function.

### Reference Types

Unlike value types, reference types are not copied when they are assigned to a variable or constant, or when they are passed to a function. Rather than a copy, a reference to the same existing instance is used.

<mark style="background-color:orange;">Classes are reference types.</mark>

### Size of a Data Type ( a data's type / a value's type :-))

The size of a data type specifies the size of data that can be stored in a given variable or constant.

A Type’s size is measured in terms of bit and can store values up to 2 bits.

For a n bit system, it can store a maximum of 2n values in it.\


Think of bit as a value that is either 0 or 1.

This philosophy is often summarized as: "Ruby is designed to make programmers happy."

Human-Centric Design: Matz designed Ruby with an emphasis on the needs of humans rather than computers, which makes it intuitive and easy to read. It emphasises natural language elements, significant whitespace, and common idioms, so Ruby code often reads like English sentences.

Flexible: Ruby is designed to be flexible to allow programmers to have multiple ways to do the same thing. This gives you the freedom to write code that best suits your thinking process.

Consistent: In Ruby, everything is an object, and all of those objects have methods. This consistent, object-oriented approach makes Ruby code easy to understand and predict. Even basic data types like integers are objects with methods.

Metaprogramming: Ruby has robust metaprogramming capabilities. This means you can write code that generates other code, making Ruby very powerful and flexible.

Blocks, Procs, and Lambdas: Ruby features first-class support for "blocks" of code and makes it easy to pass these blocks around your program. This feature is heavily used in Ruby for handling everything from basic iteration to customising how complex objects behave.\


\# A block is simply a chunk of code, and it may have arguments.

\# Here's a simple block that gets run with the \`times\` method:

5.times do |i|

puts "We are at number #{i}!"

end

\
This will output:\
We are at number 0!

We are at number 1!

We are at number 2!

We are at number 3!

We are at number 4!

WHL: 5 is an integer and an object. How can that be? With a language background of Java or Rust, it's hard to understand.

ChatGPT: Yes, the idea that everything is an object in Ruby, including primitives like integers or booleans, can be a little challenging to understand if you're coming from a language like Java or Rust where primitives are not objects.

In languages like Java or Rust, primitives such as integers or booleans are not objects, they're basic data types with a fixed size in memory and a specific set of operations that can be performed on them. They don't have methods or properties like objects do.

Ruby, however, takes a different approach. In Ruby, everything is an object. This includes integers, strings, arrays, and even classes and modules themselves. Each of these objects is an instance of a class, which means it has a set of methods it can call and it can have instance variables to hold state.

For example, an integer in Ruby is an instance of the Integer class, which means it has methods that can be called on it, like even? to check if the number is even, or times to repeat an action a certain number of times.

Here's how you can use these methods on an integer in Ruby:

ruby

Copy code

\# Here's an integer:

i = 5

\# Because \`i\` is an object, we can call methods on it:

puts i.even? # Prints 'false'

puts i.next # Prints '6'

\# We can even use a method like \`times\` to do something repeatedly:

i.times do |n|

puts "This is repetition number #{n}."

end

In this way, Ruby simplifies its model of the world by treating everything as an object, each with its own set of behaviours and data. This allows for a consistent way of interacting with all elements in the language and makes the language more flexible and expressive.





***

## Class

Classes are, at heart, a way to organise objects and methods.\
<mark style="background-color:red;">% 與其說 organise，毋寧說 define 或 design，可以說是「藍圖」。 20231117%</mark>

Defining a class lets you group behaviours (methods) into convenient bundles, so that you can quickly create many objects that behave essentially the same way.

Everything you handle in Ruby is either an object or a construct that evaluates to an object, and every object is an instance of some class.

When you use the dot notation on a class, you send a message to the class. Classes can respond to messages.

Ruby is about objects, and objects are instances of classes.

Classes are objects.

_Object_ is a built-in Ruby class.

Classes are named with constants.

% 定義一個 Class，就像「開模」來製造一個銅盤一樣。20230624 %

### Methods

Methods defined inside a class and intended for use by all instances of the class, are called instance methods.

Methods that you define for one particular object are called singleton methods.

### Variable 承值容器（可更换值的）

\#AppleScript: Variables are what we use to store objects when we aren’t working with them. Think of a variable as a box. Whenever a script has an object that it will need to use again later, it can put it in this box for safe storage while it goes off and does other things. Later on, when it needs to use that object again, it can retrieve it just by finding the box it put it in earlier. To make these storage boxes easy to identify, each one has its own name, or identifier.

WHL: If a variable is like container, say a bottle, I think, this bottle has two info on it: a name of the value, and a memory address of the value. Right?

GitHub Copilot: Yes, you are correct. In most programming languages, including C and Ruby, a variable can be thought of as a container that holds a value in memory.

So in your analogy, the bottle can be thought of as a container that holds a value, and it has two pieces of information associated with it: the name of the value (which is like the variable name), and the memory address where the value is stored (which is like the location of the bottle).

#### Instance Variable 實例變量 / 某實體中的一個值容器

Ruby objects/instances come with their own storage and retrieval mechanisms for values: instance variables. The instance variable enables individual objects to remember state.

Instance variables are only visible to the instance to which they belong.

An instance variable initialised in one method inside a class can be used by any instance method defined within that class.

Instance variable names always start with a single @ (at sign).

An instance variable retains the value assigned to it even after the method in which it was initialised has terminated. This property of instance variables - their survival across method calls — makes them suitable for maintaining state in an object.

You can change any instance variable’s value in any method.



GitHub Copilot: Class variables are typically defined at the class level, outside of any methods. For example:

class MyClass

&#x20; @@class\_variable = "Hello, world!"

end

The initialize method is used to define instance variables.

The initialize method is called when a new instance of the class is created. For example:

class MyClass

&#x20; def initialize(instance\_variable)

&#x20;   @instance\_variable = instance\_variable

&#x20; end

end

In this example, we define a class called MyClass with an initialize method that takes an argument called instance\_variable. Within the initialize method, we define an instance variable called @instance\_variable and set its value to the value of the instance\_variable argument.

GitHub Copilot:

In Ruby, an instance variable defined outside of the initialize method is not a class instance variable, but rather an instance variable that is shared by all methods of the class. This is in contrast to class instance variables, which are defined at the class level and are shared by all instances of the class.

Here's an example of how you could define an instance variable and a class instance variable in Ruby:

class MyClass

@class\_instance\_variable = "Hello, world!"

def initialize(instance\_variable)

@instance\_variable = instance\_variable

end

def say\_hello

puts @class\_instance\_variable

puts @instance\_variable

end

end

\# Create two instances of the class

my\_instance\_1 = MyClass.new("Instance 1")

my\_instance\_2 = MyClass.new("Instance 2")

\# Call the method on each instance

my\_instance\_1.say\_hello # Output: "Hello, world!" and "Instance 1"

my\_instance\_2.say\_hello # Output: "Hello, world!" and "Instance 2"

So to answer your question, an instance variable defined outside of the initialize method is not a class instance variable, but rather an instance variable that is shared by all methods of the class. An instance variable defined inside the initialize method is a regular instance variable that is unique to each instance of the class.

GitHub Copilot: In Ruby, an instance variable defined outside of the initialize method is not a class instance variable, but rather an instance variable that is shared by all methods of the class. This is in contrast to class instance variables, which are defined at the class level and are shared by all instances of the class.

Here's a table that compares class variables, instance variables, and class instance variables in Ruby:

| Variable Type                     | Definition                                                                                           | Scope                                                  | Shared by Subclasses | Prefix |
| --------------------------------- | ---------------------------------------------------------------------------------------------------- | ------------------------------------------------------ | -------------------- | ------ |
| <p>Class<br>Variable</p>          | A variable that is shared by all instances of a class and its subclasses.                            | Defined at the class level, outside of any methods.    | Yes                  | @@     |
| Instance Variable                 | A variable that is unique to each instance of a class.                                               | Defined within methods, such as the initialize method. | No                   | @      |
| <p>Class<br>Instance Variable</p> | A variable that is shared by all instances of a class, but is not shared by subclasses of the class. | Defined at the class level, outside of any methods.    | No                   | @      |



**Encapsulation** describes the fact that an object contains both its own data and the methods required to manipulate that data.

**Polymorphism** describes the ability to have different classes containing methods with the same name. The same “message” (such as talk) can be sent to different objects (such as cats and dogs), and each different object responds differently to the same message with its own special method (here the talk method).&#x20;

### Number

In Ruby, numbers are objects.

Keep in mind that most of the arithmetic operators you see in Ruby are methods. They don’t look that way because of the operator-like syntactic sugar that Ruby gives them.

If you define, say, a method called + in a class of your own, you can use the operator’s syntactic sugar.\
And if you see arithmetic operators behaving weirdly, it may be that someone has redefined their underlying methods.
