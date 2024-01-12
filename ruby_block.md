# Block, Proc, Lambda



## Block



If you have used `each` before, then you have used blocks!

A code block is a chunk of code you can pass to a method, as if the code block were another parameter. 

A code block is a set of Ruby statements and expressions inside braces or a do/end pair. 

The block may start with an argument list between vertical bars. 

==A code block may appear only immediately after a method invocation, and the start of the block (the brace or the `do`) must be on the same logical source line as the end of the invocation.==

### Why do block exist?

A block is useful because it allows you to save a bit of logic (code) & use it later.





Blocks can be “explicit” or “implicit”. Explicit means that you give it a name in the parameter list. You can pass an explicit block to another method or save it into a variable to use later.

```ruby
def broadcast( &work )
     work.call # same as yield
end
broadcast { puts "Explicit block called" }
```

Notice the `&work` paramete. That’s how you define the block’s name!

{...} is a block. do ... end is a block

****



`[2, 4, 6].select!( &:even? )` is equivalent to `[2, 4, 6].select! { |i| i.even? }`

The `&:even?` is shorthand for a block `{ |i| i.even? }`.

`:even?` is a method that returns `true` if an integer is even and `false` otherwise. The colon `:` before `even?` indicates that it is a symbol, namely, ==the `:` before `even?` converts the name of the method into a symbol.== So, `:even?` represents the symbol form of method `even?`.

==The `&` operator is used to convert the symbol `:even?` into a Proc object==, which is then passed to the `select!` method. It will allow us to call the method named `even?` on each element of the array.

Since `!` is used after `select`, it modifies the original array itself.



### `yield`

`yield` is a keyword that calls a block when you use it. It’s how methods **USE** blocks!

When you use the `yield` keyword, the code inside the block will run to do its job, just like when you call a regular method.



****

## Lambda

A lambda is a way to define a block and its parameters with some special syntax. You can save this lambda into a variable for later use.

A **Lambda** is created with `lambda {}` or `-> {}`.

```ruby
say_something = -> { puts "This is a lambda." }
talk_anything = lambda { puts "This is also a lambda." }
```

Defining a lambda won’t run the code inside it, just like defining a method won’t run the method, you need to use the `call` method for that.

### What is a lambda in general?

In general programming concepts, a lambda is ==a type of anonymous function==. The term originates from lambda calculus, a formal system in mathematical logic. 

1. **Anonymous**: Lambda functions are usually anonymous, meaning they don't have a name like traditional functions. This makes them convenient for ==short, throwaway functions== that are used only in a particular context.
2. **Concise Syntax**: Lambdas typically have a more concise syntax compared to regular functions, making them ==easier to read and write for small functionalities==.
3. **Immediate Execution**: ==Unlike regular functions, lambdas can be executed immediately at the place where they are defined.==
4. **Closure**: ==Lambdas often form closures==, meaning they can capture and use variables from their enclosing scope. This makes them powerful for various programming patterns, such as callbacks, event handlers, and short-lived operations that require some local state.



## Proc

A **Proc** is created with `proc {}` or `Proc.new {}`.



### The difference between a Proc and a Lambda

In Ruby, both Procs and Lambdas are objects belonging to the `Proc` class, and they are used to encapsulate blocks of code. 

**Lambdas** are closer to a "function" in the traditional sense. They are expected to behave like methods with respect to arguments and return values. **Procs** are more like "blocks of code" that can be executed.

Lambdas are generally preferred when you need function-like behavior, while Procs are useful for more flexible code blocks where such strictness is not required.

**Argument Handling**: 

- Lambdas check the number of arguments passed to them and will throw an error if the number of arguments does not match the expected number.
- Procs are more flexible with arguments. If you pass the wrong number of arguments to a Proc, it won't complain. If it's missing arguments, they will be set to `nil`.

**Return Behavior**:

- When you `return` from a Lambda, it returns control to the enclosing method, just like a regular method return.
- When you `return` from a Proc, it does so immediately, without going back to the calling method. This is known as a non-local return.

These differences can lead to different behaviors in code. 

A lambda 是傳統、嚴格意義上的 function。不知道，Ruby為何不直接稱之為 function。



