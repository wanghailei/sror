# Views

## form\_with

`form_with()` sets up a Ruby block environment, within which, the block’s parameter `f` is used to reference a `form` context.

Before form\_with was introduced in Rails 5.1 its functionality used to be split between form\_tag and form\_for. Both are now soft-deprecated.

### `form_with model:` Binding a Form to an Object

<mark style="background-color:orange;">The</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">`form_with model:`</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">helper sets up an HTML form that knows about Rails routes and models.</mark>

```ruby
<%= form_with model: @order do |f| %>
    <%= f.label :name, "Name:" %>
    <%= f.text_field :name, size: 40 %>
<% end %>
```

The `:model` argument of `form_with` binds the form builder object to a model object. This association means that: 1) the form will be scoped to that model object, 2)the form's fields will be populated with values from that model object, and 3) submitting the form will set the right names and values in the data available to the controller.

### form\_with and RESTful resources

When dealing with RESTful resources, calls to `form_with` can get significantly easier if you rely on record identification. In short, you can just pass the model instance and have Rails figure out model name and the rest.

The long and short style of editing an existing article have the same outcome:

```ruby
# long-style:
form_with(model: @article, url: article_path(@article), method: "patch")
# short-style:
form_with(model: @article)
```

### Parameter Naming Conventions

Values from forms can be at the top level of the `params` hash or nested in another hash. For example, in a standard `create` action for a `Person` model, `params[:person]` would usually be a hash of all the attributes for the person to create. The params hash can also contain arrays, arrays of hashes, and so on.

Fundamentally HTML forms don't know about any sort of structured data, all they generate is name-value pairs, where pairs are just plain strings. The arrays and hashes you see in your application are the result of some parameter naming conventions that Rails uses.



***

## Turbo

<mark style="background-color:green;">% 有 Turbo，可以讓 UI 局部刷新，且不用寫 Javascript。20231129 %</mark>

Turbo speeds up Rails applications, reduces the amount of JavaScript we have to write, and makes it easy to work with real-time features.

1\. All clicks on links and form submissions are now AJAX requests, thanks to Turbo Drive. We get this benefit for free as it does not require any work; we only have to import the library.

2\. It is now effortless, with just a few lines of code to build dynamic applications by slicing pages in different pieces with Turbo Frames. We develop our CRUD controllers just like we did before, and just by adding a few lines of code, we can replace or lazy-load independent parts of the page!

3\. It becomes trivial to add real-time features with the help of Turbo Streams. Want to add real-time notifications to your application, build a real-time multiplayer game, or a real-time bug monitoring system? The real-time part is just a few lines of code with Turbo Stream!

## Stimulus

Stimulus is a JavaScript framework with modest ambitions. Unlike other front-end frameworks, Stimulus is designed to enhance server-rendered HTML by connecting JavaScript objects to elements on the page using simple annotations.

These JavaScript objects are called controllers, and Stimulus continuously monitors the page waiting for HTML `data-controller` attributes to appear. For each attribute, Stimulus looks at the attribute’s value to find a corresponding controller class, creates a new instance of that class, and connects it to the element.

You can think of it this way: just like the class attribute is a bridge connecting HTML to CSS, Stimulus’s `data-controller` attribute is a bridge connecting HTML to JavaScript.

Aside from controllers, the three other major Stimulus concepts are:

\- actions, which connect controller methods to DOM events using data-action attributes

\- targets, which locate elements of significance within a controller.

Targets Map Important Elements To Controller Properties.

\- values, which read, write, and observe data attributes on the controller’s element

Stimulus’s use of data attributes helps separate content from behaviour in the same way CSS separates content from presentation.

<mark style="background-color:orange;">Stimulus helps you build small, reusable controllers, giving you just enough structure to keep your code from devolving into “JavaScript soup.”</mark>



