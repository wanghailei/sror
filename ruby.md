# Ruby lang

This philosophy is often summarized as: "Ruby is designed to make programmers happy."

Human-Centric Design: ==Matz designed Ruby with an emphasis on the needs of humans rather than computers==, which makes it intuitive and easy to read. It emphasises natural language elements, significant whitespace, and common idioms, so Ruby code often reads like English sentences.

Flexible: Ruby is designed to be flexible to allow programmers to have multiple ways to do the same thing. This gives you the freedom to write code that best suits your thinking process.

Consistent: In Ruby, ==everything is an object, and all objects have methods==. Even basic data types like integers are objects with methods.

Metaprogramming: Ruby has robust metaprogramming capabilities. This means you can write code that generates other code, making Ruby very powerful and flexible.

Blocks, Procs, and Lambdas: Ruby features first-class support for "blocks" of code and makes it easy to pass these blocks around your program. This feature is heavily used in Ruby for handling everything from basic iteration to customising how complex objects behave.



## OO

**Encapsulation** describes the fact that an object contains both its own data and the methods required to manipulate that data.

**Polymorphism** describes the ability to have ==different classes containing methods with the same name==. The same “message” can be sent to different objects, and ==each different object responds differently to the same message with its own special method==. For example, the same messsage or command "talk" is sent to a cat and a dog, and the cat and the dog responds differently to this message.





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

==我認為 type 翻譯成「形態」/「型態」比較合適，甚至叫「形狀」或「模樣」都很好。因為一個 type 確實表現的是一段代碼的構成樣式、形狀、構造，如果這種樣式經常被看到，就可以抽象出來，並起一個名字，也就是稱之為「某型代碼」或「某種形態代碼」。這跟虎形、鶴形；可愛型、性感型，其實是一個道理。==

==形，外形、姿態、容貌、樣式等意，例如：形勢、形色、形式等。型，器物的模樣，引申為某種標準，型式、典範、態度、風格之意。例如：模型、典型。二字意思相近，有字典謂兩字相通。所以，凡與外貌有關的，用「形」字；凡人工鑄造出來的，或引申事物表現的格調，用「型」字。==

==英文的「形」為shape；英文的「型」為type、style。==

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

==Classes are reference types.==

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

Blocks, Procs, and Lambdas: Ruby features first-class support for "blocks" of code and makes it easy to pass these blocks around your program. This feature is heavily used in Ruby for handling everything from basic iteration to customising how complex objects behave.


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



&#x20;

### Number

In Ruby, numbers are objects.

Keep in mind that most of the arithmetic operators you see in Ruby are methods. They don’t look that way because of the operator-like syntactic sugar that Ruby gives them.

If you define, say, a method called + in a class of your own, you can use the operator’s syntactic sugar.\
And if you see arithmetic operators behaving weirdly, it may be that someone has redefined their underlying methods.



`# frozen_string_literal: true`: This line is a magic comment in Ruby. It tells Ruby to freeze all string literals in the file. Freezing a string makes it immutable, meaning it can't be modified.

***





