> To learn the difference btw Unit testing, TDD and BDD please have a look at [this article](https://codeutopia.net/blog/2015/03/01/unit-testing-tdd-and-bdd/)
# From [Semaphore](https://semaphoreci.com/community/tutorials/getting-started-with-rspec)

## Getting Started with RSpec

Instead of always writing tests for some code we already have, we work in a red-green loop:

1. Write the smallest possible test case that matches what we need to program.
2. Run the test and watch it fail. This gets you into thinking how to write only the code that makes it pass.
3. Write some code with the goal of making the test pass.
4. Run your test suite. Repeat steps 3 and 4 until all tests pass.
5. Go back and refactor your new code, making it as simple and clear as possible while keeping the test suite green.

Behavior-driven development is a concept built on top of TDD. The idea is to write tests as *specifications of system behavior*.  It is about a different way of approaching the same challenge, which leads us to think more clearly and write tests that are easier to understand and maintain. This in turn helps us write better implementation code.

## RSpec Basics

### Setting Up RSpec

Let's start a new Ruby project where we'll configure RSpec as a dependency via [Bundler](http://bundler.io/). Create a new directory and put the following code in your `Gemfile`:

```
# Gemfile
source "https://rubygems.org"

gem "rspec"
```
Open your project's directory in your terminal, and type `bundle install --path .bundle` to install the latest version of RSpec and all related dependencies.

### Writing the First Spec

By convention, tests written with RSpec are called "specs" (short for "specifications") and are stored in the project's `spec` directory.

```
# spec/string_calculator_spec.rb
describe StringCalculator do
end
```

With RSpec, we are always *describing* the behavior of classes, modules and their methods. The describe block is always used at the top to put specs in a context. It can accept either a class name, in which case the class needs to exist, or any string you'd like.

To run the specs, type:

```
bundle exec rspec
```

Do this now, and our spec will fail with the `uninitialized constant StringCalculator (NameError)` error. That's expected, as we haven't created that class yet.

Create a new directory called `lib`:

```
mkdir lib
```
Declare `StringCalculator` in `string_calculator.rb`:

```
# lib/string_calculator.rb
class StringCalculator
end
```
And require it in your spec:

```
# spec/string_calculator_spec.rb
require "string_calculator"

describe StringCalculator do
end
```

Running RSpec now passes:

```
$ bundle exec rspec
No examples found.


Finished in 0.00068 seconds (files took 0.30099 seconds to load)
0 examples, 0 failures
```
That means we are ready to add code.

```
# spec/string_calculator_spec.rb
describe StringCalculator do

  describe ".add" do
    context "given an empty string" do
      it "returns zero" do
        expect(StringCalculator.add("")).to eql(0)
      end
    end
  end
end
```

- We are using another `describe` block to describe the `add` class method. By convention, class methods are prefixed with a dot (`".add"`), and instance methods with a hash (`"#add"`).

- We are using a `context` block to describe the context under which the `add` method is expected to return zero. `context` is technically the same as `describe`, but is used in different places, to aid reading of the code.

- We are using an `it` block to describe a specific *example*, which is RSpec's way to say "test case". Generally, every example should be descriptive, and together with the context should form an understandable sentence. This one reads as "add class method: given an empty string, it returns zero".

- `expect(...).to` and the negative variant `expect(...).not_to` are used to define expected outcomes. The Ruby expression they are given (in our case, `StringCalculator.add("")`) is combined with a *matcher* to fully define an *expectation* on a piece of code. The matcher we are using here is *eql*, a basic equality matcher. RSpec comes with [many more matchers](https://relishapp.com/rspec/rspec-expectations/v/3-1/docs/built-in-matchers).

If we run our spec now, we will get a failure that the method is not defined. Let's make that spec pass:

```
# lib/string_calculator.rb
class StringCalculator

  def self.add(input)
    0
  end
end
```
If you run `bundle exec rspec` now, the spec does pass.

### Towards Working Code

```
# spec/string_calculator_spec.rb
describe StringCalculator do

  describe ".add" do
    context "given '4'" do
      it "returns 4" do
        expect(StringCalculator.add("4")).to eql(4)
      end
    end

    context "given '10'" do
      it "returns 10" do
        expect(StringCalculator.add("10")).to eql(10)
      end
    end
  end
end
```

After we have run the specs, we will get some helpful outputas listed failures. We make them pass:

```
# lib/string_calculator.rb
class StringCalculator

  def self.add(input)
    if input.empty?
      0
    else
      input.to_i
    end
  end
end
```
These specs fail, as you'd expect. Here's one way to make the specs pass:

```
class StringCalculator

  def self.add(input)
    if input.empty?
      0
    else
      numbers = input.split(",").map { |num| num.to_i }
      numbers.inject(0) { |sum, number| sum + number }
    end
  end
end
```

> RSpec has more than one way to display its output. A very popular alternative to the default dot format is the "documentation" format: `bundle exec rspec --format documentation`

## Test Subjects

Let's say that we need to write a simple program for runners who need to log their runs and are interested in seeing some weekly statistics. Basic information about a run includes distance, duration and when it happened. There should be a class `Run` with three attributes:

```
describe Run do

  describe "attributes" do

    subject do
      Run.new(:duration => 32,
              :distance => 5.2,
              :timestamp => "2014-12-22 20:30")
    end

    it { is_expected.to respond_to(:duration) }
    it { is_expected.to respond_to(:distance) }
    it { is_expected.to respond_to(:timestamp) }
  end
end
```

In this example we declare a *subject* to be an instance of class `Run`. The reason why we define it is that we have multiple test examples that work with the same test subject. RSpec understands it as an object which should [respond_to](http://ruby-doc.org/core-2.2.0/Object.html#method-i-respond_to-3F) (in core Ruby sense) a number of methods, such as `duration`. The expectation is using RSpec's built-in `respond_to` matcher.

The one-line syntax shown above is convenient when you can avoid duplication between a matcher and the string that documents the test example. If this were not possible, we would need to write the examples above like this:

```
it "responds to '#duration'" do
  expect(subject).to respond_to(:duration)
end
```
In fact, if our objects can be initialized without parameters, we can make it even shorter:

```
describe Run do
  it { is_expected.to respond_to(:duration) }
end
```
This is because we passed the class to the `describe` block and RSpec has already initialized a subject in the global example group to be `subject { Run.new }`.

Subjects can also be referenced explicitly, via `subject`:

```
describe Run do
  subject do
    Run.new(:duration => 32,
            :distance => 5.2,
            :timestamp => "2014-12-22 20:30")
  end

  describe "#timestamp" do
    it "returns a DateTime" do
      expect(subject.timestamp).to be_a(DateTime)
    end
  end
end
```
> However, we recommend that you do not use `subject` like this. There are other ways which reveal the intent of code more clearly, as we will see below.

## Before Hooks

Let's say that we are describing a method that should return the total number of logged runs: `Run.count`. This method can also optionally receive a parameter to limit the scope to one week. Before we call it, we need to log a number of runs first.

RSpec's `before` hook is a convenient way to structure code which should run before every example, as in the following spec:

```
describe RunningWeek do

  describe ".count" do

    context "with 2 logged runs this week and 1 in next" do

      before do
        2.times do
          Run.log(:duration => rand(10),
                  :distance => rand(8),
                  :timestamp => "2015-01-12 20:30")
        end

        Run.log(:duration => rand(10),
                :distance => rand(8),
                :timestamp => "2015-01-19 20:30")
      end

      context "without arguments" do
        it "returns 3" do
          expect(Run.count).to eql(3)
        end
      end

      context "with :week set to this week" do
        it "returns 2" do
          expect(Run.count(:week => "2015-01-12")).to eql(2)
        end
      end
    end
  end
end
```

When you write `before`, it is the equivalent of writing `before(:each)`, which means "run this code before each example". You can also say `before(:all)` which would run the code only once for the given context. If you need, you can also define an `after` hook, with the same variants. You can read more about hooks in [RSpec documentation](https://semaphoreci.com/community/tutorials/rspec-subject-helpers-hooks-and-exception-handling).


## Let Helper

RSpec's `let` helper is a way to define all dependent objects for test examples. If you need to reference the same "thing" in more than one example, and it cannot be made a `subject`, that is a good use case for `let`.

The code that is placed inside a `let` block is lazily evaluated: it is executed only the first time a test example calls it and is cached for further calls in the same example. If you need to force the method to be invoked every time, use `let!`

```
describe RunningWeek do

  let(:monday_run) do
    Run.new(:duration => 32,
            :distance => 5.2,
            :timestamp => "2015-01-12 20:30")
  end

  let(:wednesday_run) do
    Run.new(:duration => 32,
            :distance => 5.2,
            :timestamp => "2015-01-14 19:50")
  end

  let(:runs) { [monday_run, wednesday_run] }

  let(:running_week) { RunningWeek.new(Date.parse("2015-01-12"), runs) }

  describe "#runs" do

    it "returns all runs in the week" do
      expect(running_week.runs).to eql(runs)
    end
  end

  describe "#first_run" do

    it "returns the first run in the week" do
      expect(running_week.first_run).to eql(monday_run)
    end
  end

  describe "#average_distance" do

    it "returns the average distance of all week's runs" do
      expect(running_week.average_distance).to be_within(0.1).of(5.4)
    end
  end
end
```
Contrast this code with the example for the `before` hook, where we needed to prepare some data but did not care about it later. In this spec we need to both prepare some data and easily reference it in test examples.

> Also, note the use of [composed matchers](https://relishapp.com/rspec/rspec-expectations/v/3-1/docs/composing-matchers) in the last example (be_within(...).of(...)). RSpec's matchers can be composed, which helps improve code readability. If you are interested in seeing the full list of matchers that exist and can be composed, browse the documentation of classes and methods in `RSpec::Matchers::BuiltIn`.

## Instance Variables in Before Hooks vs Let

At this point you may be wondering why not just use instance variables in `before` blocks instead of `let`:

```
describe RunningWeek do
  before do
    @monday_run = Run.new(...)
  end
end
```

There are actually three approaches to the extent of the use of `let`:

1. Use `let` to define all object dependencies and keep the body of examples minimal.
2. Use it occasionally to avoid duplication by defining "variables" when in need to reference the same thing in multiple test examples, but not much more.
3. Not using it at all; relying on instance variables in `before` hooks only.

We encourage you to adopt the first approach, combined with additional data setup in a `before` hook when necessary. It results in very readable code, is less error-prone (typos in instance variables do not raise exceptions) and may give better performance due to lazy evaluation. RSpec maintainer Myron Marston [recommends it](https://stackoverflow.com/questions/5359558/when-to-use-rspec-let/5359979#5359979) as well.

## Exception Handling

We often need to specify that a given method or block of code should raise an exception. For this purpose you can use the `raise_error` matcher (or its equivalent, `raise_exception`):

```
describe RunningWeek do

  describe "initialization" do

    context "given a date which is not a Monday" do

      it "raises a 'day not Monday' exception" do
        expect { RunningWeek.new(Date.parse("2015-01-13"), []) }.to raise_error("Day is not Monday")
      end
    end
  end
end
```

## Mocking with RSpec: Doubles and Expectations

### Introduction

Mocking is a technique in test-driven development (TDD) that involves using fake dependent objects or methods in order to write a test. There are a couple of reasons why you may decide to use mock objects:

- As a replacement for objects that don't exist yet.
- When you are working with objects which return non-deterministic values or depend on an external resource, e.g. a method that returns an RSS feed from a server.
- To avoid setting up a complex scheme of data or dependency objects in order to write a test.
- To avoid invoking code which would degrade the performance of the test, while at the same time being unrelated to the test you are writing.

The first reason is particularly prevalent among those who practice behavior-driven development (BDD).

By mocking objects in advance, you can allow yourself to focus on the thing that you're working on at the moment. Let's say that you are working on a new part of the system, and you realize that the code you're currently describing and implementing will require two new collaborating objects. Using mocks, you can define their interfaces as you write a spec for the code you're currently working on.

That way, you maintain a clean environment by having all your tests pass, before moving on to implement the collaborating objects. Without mocks, you'd be required to immediately jump to writing the implementation for the collaborating objects, before having your tests pass. This can be distracting and may lead to poor code design decisions. Mocking helps us by reducing the number of things we need to keep in our head at a given moment.

Mocking with RSpec is done with the [rspec-mocks](https://github.com/rspec/rspec-mocks) gem. If you have `rspec` as a dependency in your `Gemfile`, you already have rspec-mocks available.

## Doubles

A *test double* is a simplified object which takes the place of another object in a test. Creating a double with RSpec is easy:

```
feed = double

# Optionally, you may give your double an identifier, which may come handy
# when debugging and inspecting objects:
feed = double("feed")
```

### Method Stubs

A new double resembles a plain Ruby `Object` — it's not very useful on its own. It is usually the first step before defining some fake methods on it. This is called *method stubbing*, and with RSpec 3 it is done using the `allow()` and `receive()` methods:

```
allow(feed).to receive(:fetch).and_return("imagine I'm a JSON string")

feed.fetch
=> "imagine I'm a JSON string"
```

The value provided to `and_return()` defines the return value of the stubbed method. The use of `and_return()` is optional, and if you don't have it, the stubbed method will be set to return `nil`.

You can also apply `allow` to a real object (which is not a double). When testing Rails applications, for example, it is common to mock a method which works with the database and make it return a predefined double whenever the focus of the code is not whether the database operations work or not (and the test can run faster too).

```
comment = double("comment")
expect(Comment).to receive(:find).and_return(comment)
```

### Message Expectations

Expecting messages — that is, defining expectations on test doubles that certain methods will be invoked after some code that follows runs — is a common pattern when working with doubles.

> Please visit the [link](https://semaphoreci.com/community/tutorials/mocking-with-rspec-doubles-and-expectations) to see the rest of the article

# Better Specs [Documentation](http://www.betterspecs.org/)

- **Use contexts**

```
# BAD

it 'has 200 status code if logged in' do
  expect(response).to respond_with 200
end
it 'has 401 status code if not logged in' do
  expect(response).to respond_with 401
end

# GOOD

context 'when logged in' do
  it { is_expected.to respond_with 200 }
end
context 'when logged out' do
  it { is_expected.to respond_with 401 }
end
```
When describing a context, start its description with "when" or "with".

- **Single expectation test**

In isolated unit specs, you want each example to specify one (and only one) behavior. Multiple expectations in the same example are a signal that you may be specifying multiple behaviors.

Anyway, in tests that are not isolated (e.g. ones that integrate with a DB, an external webservice, or end-to-end-tests), you take a massive performance hit to do the same setup over and over again, just to set a different expectation in each test. In these sorts of slower tests, I think it's fine to specify more than one isolated behavior.

```
# GOOD(ISOLATED)

it { is_expected.to respond_with_content_type(:json) }
it { is_expected.to assign_to(:resource) }

# GOOD(NOT ISOLATED)

it 'creates a resource' do
  expect(response).to respond_with_content_type(:json)
  expect(response).to assign_to(:resource)
end
```

- **Test all possible cases**

```
# Destroy Action

before_filter :find_owned_resources
before_filter :find_resource

def destroy
  render 'show'
  @consumption.destroy
end
```
The error I usually see lies in testing only whether the resource has been removed. But there are at least two edge cases: when the resource is not found and when it's not owned.

```
# BAD

it 'shows the resource'

# GOOD

describe '#destroy' do

  context 'when resource is found' do
    it 'responds with 200'
    it 'shows the resource'
  end

  context 'when resource is not found' do
    it 'responds with 404'
  end

  context 'when resource is not owned' do
    it 'responds with 404'
  end
end
```

- **Expect vs Should syntax**

On new projects always use the expect syntax.

```
# BAD

it 'creates a resource' do
  response.should respond_with_content_type(:json)
end

# GOOD

it 'creates a resource' do
  expect(response).to respond_with_content_type(:json)
end
```

- **Use subject**

If you have several tests related to the same subject use `subject{}` to DRY them up.

```
# BAD

it { expect(assigns('message')).to match /it was born in Belville/ }

# GOOD

subject { assigns('message') }
it { is_expected.to match /it was born in Billville/ }

# GOOD

subject(:hero) { Hero.first }
it "carries a sword" do
  expect(hero.equipment).to include "sword"
end
```
RSpec has also the ability to use a named subject.

- **Use let and let!**

When you have to assign a variable instead of using a `before` block to create an instance variable, use `let`. Using `let` the variable lazy loads only when it is used the first time in the test and get cached until that specific test is finished. A really good and deep description of what `let` does can be found in this [stackoverflow answer](https://stackoverflow.com/questions/5359558/when-to-use-rspec-let/5359979#5359979).

```
# BAD

describe '#type_id' do
  before { @resource = FactoryGirl.create :device }
  before { @type     = Type.find @resource.type_id }

  it 'sets the type_id field' do
    expect(@resource.type_id).to equal(@type.id)
  end
end

# GOOD

describe '#type_id' do
  let(:resource) { FactoryGirl.create :device }
  let(:type)     { Type.find resource.type_id }

  it 'sets the type_id field' do
    expect(resource.type_id).to equal(type.id)
  end
end

# Use `let` to initialize actions that are lazy loaded to test your specs.
# GOOD

context 'when updates a not existing property value' do
  let(:properties) { { id: Settings.resource_id, value: 'on'} }

  def update
    resource.properties = properties
  end

  it 'raises a not found error' do
    expect { update }.to raise_error Mongoid::Errors::DocumentNotFound
  end
end

# Use `let!` if you want to define the variable when the block is defined. This can be useful to populate your database to test queries or scopes.


# GOOD
# Here an example of what let actually is.
# this:
let(:foo) { Foo.new }

# is very nearly equivalent to this:
def foo
  @foo ||= Foo.new
end
```

- **Mock or not to mock**

There's a debate going on. Do not (over)use mocks and test real behavior when possible. Testing real cases are useful when updating your application flow.

```
# simulate a not found resource
context "when not found" do
  before { allow(Resource).to receive(:where).with(created_from: params[:id]).and_return(false) }
  it { is_expected.to respond_with 404 }
end
```
Mocking makes your specs faster but they are difficult to use. You need to understand them well to use them well. Read more [about](http://myronmars.to/n/dev-blog/2012/06/thoughts-on-mocking).

> Please visit the [link](http://www.betterspecs.org/) to see the rest of the article



> hmm it must be trying to load the spec_helper file in the rspec gem. This is a non typical set up, usually test files are in a spec folder. It should be easy enough to fix this though.
run `rspec --init` in your terminal
that will generate a `spec_helper.rb` file and a `spec/` folder
then move your `caesar_spec.rb` into the generated `spec` folder.

### From Michael Hartl's [rails tutorial](https://www.railstutorial.org/book/static_pages)

In practice, we’ll usually write controller and model tests first and integration tests (which test functionality across models, views, and controllers) second. And when we’re writing application code that isn’t particularly brittle or error-prone, or is likely to change (as is often the case with views), we’ll often skip testing altogether.

We’ll write simple tests for each of the titles by combining the tests with the `assert_select` method, which lets us test for the presence of a particular HTML tag (sometimes called a “selector”, hence the name):

```
assert_select "title", "Home | Ruby on Rails Tutorial Sample App"
```
In particular, the code above checks for the presence of a `<title>` tag containing the string “Home | Ruby on Rails Tutorial Sample App”.

```
# test/controllers/static_pages_controller_test.rb

require 'test_helper'

class StaticPagesControllerTest < ActionDispatch::IntegrationTest

  test "should get home" do
    get static_pages_home_url
    assert_response :success
    assert_select "title", "Home | Ruby on Rails Tutorial Sample App"
  end

  test "should get help" do
    get static_pages_help_url
    assert_response :success
    assert_select "title", "Help | Ruby on Rails Tutorial Sample App"
  end

  test "should get about" do
    get static_pages_about_url
    assert_response :success
    assert_select "title", "About | Ruby on Rails Tutorial Sample App"
  end
end

```

The base title, “Ruby on Rails Tutorial Sample App”, is the same for every title test. Using the special function `setup`, which is automatically run before every test, verify that the tests are still green.

```
require 'test_helper'

class StaticPagesControllerTest < ActionDispatch::IntegrationTest

  def setup
    @base_title = "Ruby on Rails Tutorial Sample App"
  end

  test "should get home" do
    get static_pages_home_url
    assert_response :success
    assert_select "title", "Home | #{@base_title}"
  end

  ...
end

```

The technique involves using *embedded Ruby* in our views. Since the Home, Help, and About page titles have a variable component, we’ll use a special Rails function called `provide` to set a different title on each page. We can see how this works by replacing the literal title “Home” in the `home.html.erb` view with the code in the following

```
# app/views/static_pages/home.html.erb

<% provide(:title, "Home") %>
<!DOCTYPE html>
<html>
  <head>
    <title><%= yield(:title) %> | Ruby on Rails Tutorial Sample App</title>
  </head>
  <body>
    <h1>Sample App</h1>
    <p>
      This is the home page for the
      <a href="http://www.railstutorial.org/">Ruby on Rails Tutorial</a>
      sample application.
    </p>
  </body>
</html>
```
This is our first example of embedded Ruby, also called *ERb*. (Now you know why HTML views have the file extension .html.erb.) ERb is the primary template system for including dynamic content in web pages. The code

```
<% provide(:title, "Home") %>
```
indicates using `<% ... %>` that Rails should call the `provide` function and associate the string `"Home"` with the label `:title`. Then, in the title, we use the closely related notation `<%= ... %>` to insert the title into the template using Ruby’s `yield` function:

(The distinction between the two types of embedded Ruby is that `<% ... %>` *executes* the code inside, while `<%= ... %>` executes it and *inserts* the result into the template.) The resulting page is exactly the same as before, only now the variable part of the title is generated dynamically by ERb.


### Advanced testing setup

#### minitest reporters

To get the default Rails tests to show red and green at the appropriate times, I recommend adding the code below to your test helper file, thereby making use of the [minitest-reporters](https://github.com/kern/minitest-reporters) gem included in Gemfile.

```
# test/test_helper.rb

ENV['RAILS_ENV'] ||= 'test'
require File.expand_path('../../config/environment', __FILE__)
require 'rails/test_help'
require "minitest/reporters"
Minitest::Reporters.use!

class ActiveSupport::TestCase
  # Setup all fixtures in test/fixtures/*.yml for all tests in alphabetical order.
  fixtures :all

  # Add more helper methods to be used by all tests here...
end
```

> The code above mixes single- and double-quoted strings. This is because `rails new` generates single-quoted strings, whereas the minitest reporters documentation uses double-quoted strings. This mixing of the two string types is common in Ruby.

#### Guard

One annoyance associated with using the `rails test` command is having to switch to the command line and run the tests by hand. To avoid this inconvenience, we can use [Guard](https://github.com/guard/guard) to automate the running of the tests. Guard monitors changes in the filesystem so that, for example, when we change the static_pages_controller_test.rb file, only those tests get run. Even better, we can configure Guard so that when, say, the home.html.erb file is modified, the static_pages_controller_test.rb automatically runs.

After making Gemfile include the `guard` gem, to get started we need to initialize it:

```
$ bundle exec guard init
Writing new Guardfile to /home/ec2-user/environment/sample_app/Guardfile
00:51:32 - INFO - minitest guard added to Guardfile, feel free to edit it
```

We then edit the resulting `Guardfile` so that Guard will run the right tests when the integration tests and views are updated. (For maximum flexibility, I recommend using the version of the Guardfile listed in the [reference](http://railstutorial.org/guardfile) application).
Here is the line:

```
# A custom Guardfile

guard :minitest, spring: "bin/rails test", all_on_start: false do
```

This line causes Guard to use the Spring server supplied by Rails to speed up loading times, while also preventing Guard from running the full test suite upon starting.

To prevent conflicts between Spring and Git when using Guard, you should add the `spring/` directory to the `.gitignore` file used by Git to determine what to ignore when adding files or directories to the repository.

```
#  Adding Spring to the .gitignore file.

...

# Ignore Spring files.
/spring/*.pid

```

The Spring server is still a little quirky as of this writing, and sometimes Spring *processes* will accumulate and slow performance of your tests. If your tests seem to be getting unusually sluggish, it’s thus a good idea to inspect the system processes and kill them if necessary

> **Unix Processes**

> On Unix-like systems such as Linux and macOS, user and system tasks each take place within a well-defined container called a *process*. To see all the processes on your system, you can use the `ps` command with the `aux` options:

  ```
  $ ps aux

  $ ps aux | grep spring
  ec2-user 12241 0.3 0.5 589960 178416 ? Ssl Sep20 1:46
  spring app | sample_app | started 7 hours ago
  ```

> The result shown gives some details about the process, but the most important thing is the first number, which is the *process id*, or pid. To eliminate an unwanted process, use the `kill` command to issue the Unix termination signal (which [happens to be 15](https://en.wikipedia.org/wiki/Unix_signal)) to the pid:

  ```
  $ kill -15 12241
  ```

> This is the technique I recommend for killing individual processes, such as a rogue Rails server (with the pid found via `ps aux | grep server`), but sometimes it’s convenient to kill all the processes matching a particular process name, such as when you want to kill all the `spring` processes gunking up your system. In this particular case, you should first try stopping the processes with the `spring` command itself:

  ```
  $ spring stop
  ```

> Sometimes this doesn’t work, though, and you can kill all the processes with name `spring` using the `pkill` command as follows:

  ```
  $ pkill -15 -f spring
  ```

> Any time something isn’t behaving as expected or a process appears to be frozen, it’s a good idea to run ps aux to see what’s going on, and then run `kill -15 <pid> or pkill -15 -f <name>` to clear things up.

> Once Guard is configured, you should open a new terminal and run it at the command line as follows:

```
bundle exec guard
```

> To run *all* the tests, hit return at the `guard>` prompt. (This may sometimes give an error indicating a failure to connect to the Spring server. To fix the problem, just hit return again.)To exit Guard, press Ctrl-D.


