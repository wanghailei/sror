# Reading Rails' source code



***

## **`class << self`**

This syntax is used in Ruby to define class methods within the block. It opens up the singleton class of the current class, allowing you to define methods that will be available on the class itself, rather than on instances of the class.

Using the singleton class (`class << self`) to define class methods, groups them together makes the class more organised.

<pre class="language-ruby" data-full-width="false"><code class="lang-ruby"><strong>class MyClass
</strong>    class &#x3C;&#x3C; self
        def my_class_method
            # method implementation
        end
    end
end
</code></pre>

Using `self.` prefix, is another way, which is clear and concise, easy to read and understand.

```ruby
class MyClass
    def self.my_class_method
        # method implementation
    end
end
```



## `subclass = Class.new(self)`

`Class.new` is a method in Ruby that creates a new class.

* when you call `Class.new` without any arguments, it creates an anonymous class with `Object` as its superclass.
* when you provide an argument to \``Class.new`\`, it creates a new class with the provided argument as its superclass.
* when you pass \``self`\` as an argument to \``Class.new`\`, it creates a new class that is a subclass of the current class (the one where this code is being executed).

This subclass inherits all the methods and properties of the original class but is a distinct class that can be modified independently.

This is a way to dynamically create a new subclass of the current class. This technique is useful in scenarios where you need to create classes dynamically based on runtime conditions or for advanced metaprogramming patterns.



## `super()`

When `super()` is used in an instance method, a method of the same name but in the superclass of the current class is called. This is often used in method overrides, where you want to augment or modify the behavior of a method inherited from the superclass, not replace it entirely.

* If you use \``super()`\` with parentheses and no arguments, it calls the superclass method without any arguments, regardless of what arguments were passed to the child method.
* <mark style="background-color:orange;">If you use \`</mark><mark style="background-color:orange;">`super`</mark><mark style="background-color:orange;">\` without parentheses and arguments, it automatically forwards the arguments that were passed to the child method.</mark>

For example:

```ruby
class Animal
    def speak
        "Some generic sound"
    end
end
class Dog < Animal
    def speak
        "#{super()} and then barks"
    end
end
dog = Dog.new
puts dog.speak # Output: "Some generic sound and then barks"
```

Inside the \`speak\` method of \`Dog\`, \`super()\` is called, which invokes the \`speak\` method of \`Animal\`. The \`Dog\`'s \`speak\` method then augments this by adding "and then barks" to the string.



## `ensure`

```ruby
def a_method
    do_something
ensure
    do_others
end
```

The `ensure` block is used in conjunction with `begin`, `rescue`, and <mark style="background-color:orange;">`def`</mark> blocks to guarantee that certain code runs regardless of whether an exception occurs. The ensure block is executed after the main body of the block (or method, if used within a method definition) and after any rescue blocks, if present. It's typically used for cleanup code that you want to execute no matter what, like closing files or releasing resources.

This method demonstrates a common pattern in Ruby (and specifically Ruby on Rails), where temporary changes are made to the state, and an ensure block is used to guarantee that the original state is restored, maintaining the integrity and consistency of the application state.

## Why there is a underscore at the beginning of a method name?

`def _prepare_context`&#x20;

In Ruby, a method name beginning with an underscore (`_`) is typically and just a convention used by developers as an additional visual cue to indicate that a method is intended for internal use within the class or module. It's only a naming convention and not a language feature. The underscore does not change the visibility of the method.

For example, in Rails, methods that are not intended to be actions in a controller might be prefixed with an underscore to differentiate them from action methods.
