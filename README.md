# Intro to Tests

## Learning Goals
+ Explain the importance of test automation in code
+ Use tests to guide the flow of developing an application
+ Explore the RSpec testing environment
+ Use a pre-written test to determine what a method should do or return

## Lesson
+ Hi folks, this is Ian from Flatiron School. In this video, we're going to look at Testing and Test Driven Development.
+ Our learning goals for this video:
  + We'll explain the importance of test automation in code
  + We will use tests to guide the flow of developing an application
  + We'll explore the RSpec testing environment
  + Also we'll use a pre-written test to determine what a method should do or return
+ So, to summarize, our goal is really that you can understand the importance of tests, and read tests when doing labs.

### Intro to Testing

+ So let's get started. A lot of times, when you're writing software, you're defining code in one part of your app that actually gets used someplace else in the application.
+ So, you might be on a team of dozens of people, and you might be working on something, maybe a method, and someone else is going to use that method in the code that they are working on.
+ So most larger-scale apps have a bunch of files that define things, then other files to use what was defined.
+ Here's an simple example - in this file called `conversions`, I've defined a method called `ounces_to_grams`. This method takes in a number of ounces, and should return how many grams that weights.
+ How might we test this to make sure it works properly?
+ We could call the method in IRB and try some stuff out - I could pass in 0 and make sure it returns 0.0, or pass in 1 or 2 and make sure it returns what we think it should.
+ But, other developers won't have a lot of confidence in this method because they won't know how to test it. Likewise, it will be tough to ever change the implementation here, because we could end up breaking something.
+ So, programmers often times will write code to test their code - it's a little bit meta, but it can work really well.
+ Let's do this first in a very basic way, then we'll use a testing library to help us.
+ First, let's  make a file that we can run that will test this method for us
  + `touch`conversions_test.rb`
+ Next, in this test file, Write a simple statement to check the answer and see if the test failed or not. First, I'll require the other file
```ruby
require_relative './conversions.rb'
```
+ Next, I'll just print out what our test is going to be. So, let's start with a simple one, which is that if we pass in 0, I expect that the method should return 0.0.
+ So this is a basic test, but we'll make sure that this one works first.
```ruby
require_relative './conversions.rb'
puts "ounces_to_grams when given 0, returns 0.0"
answer = ounces_to_grams(0)
if answer == 0.0
  puts "Passed the test!"
else
  puts "Failed the test: got #{answer} instead"
end
```
+ So, first we're going to simply call the method here, and save the return value in a variable.
+ We then setup a simple conditional - if the answer == 0.0, then we print that we passed the test. Otherwise, we print what we got instead.
+ Run this file now - and we can see that this worked. So we can add more tests now - I can add one that says given 1, we should get 28.3495
```ruby
require_relative './conversions.rb'

puts "Given 0, it should return 0.0"
answer = ounces_to_grams(0)
if answer == 0.0
  puts "Passed!"
else
  puts "Test failed: got #{answer} instead"
end

puts "Given 1, it should return 28.3495"
answer = ounces_to_grams(1)
if answer == 28.3495
  puts "Passed!"
else
  puts "Test failed: got #{answer} instead"
end
```
+ Awesome, so we now have this automated test suite - and I can use this to make sure that, if we make any changes to the code, that the method still does what it's supposed to do. Let's change that method now:
  ```ruby
  GRAMS_PER_OUNCE = 28.3495
  def ounces_to_grams(ounces)
    ounces.to_f * GRAMS_PER_OUNCE
  end
  ```
+ Run our test suite - and look at that, all our tests still pass, so we know that this method does what it's supposed to do.
+ So this is great, we just used our programming knowledge to write some tests.

### RSpec

+ This is our first intro to automated testing - and naturally this test is a bit hard to write and read.
+ There's a lot of repetition here with the setup, and the expectation is a bit tough here too.
+ Instead, we can use a gem for this. A gem, or library, is just some prewritten code designed to be used in other programs.
+ The idea is that you can easily include some pre-defined methods and files in your applications.
+ We here at Flatiron School really like a library called RSpec for Ruby - it has a nice, readable syntax and it easy to use.
+ So, to get started, I need to install this gem. Here in the Learn IDE, I know that it's already installed, but if I were working on a computer that didn't have it, I could install it by doing `gem install rspec`
+ And now, I can set this project up as an rspec project by running `rspec --init `
+ What did that do? Well, let's take a look here. This created two files - the first is a `.rspec` file. This file contains some options for how we run our tests.
+ The second file is in a directory called `spec` called `spec_helper`. This file has a bunch of configuration options.
+ I can see in my RSpec file that by default, we'll include this file every time we run rspec, which is great.
+ So to run all of our tests, I can simply run `rspec` from the terminal - and this will look at every file in the spec directory that ends in `_spec` and run it for me.
+ So by convention, we name our rspec files to match the filename that we're testing, and add underscore-spec to the end. So in my case, I'm testing this file called `conversions.rb`, so I'm going to make a file called `conversions_spec.rb`
+ And just for fun, as a demo - I'll just put a puts statement in that file. `puts "Tests are running..."`
+ From my terminal now, I'll run `rspec` - and let's take a look at this output.
+ So I see my puts statement got printed here - then I see "No Examples Found", which makes sense because I haven't written any tests.
+ So let's write one - RSpec has a few built in methods that we can use to write tests. One big advantage to using rspec is that we can give ourselves some organization.
+ First, let's create a describe block. This should be a high level description of what we're testing.
```ruby
describe "conversions" do

end
```
+ We can also nest these blocks to have different descriptions. In this case, I'll make a second one to describe the method name we're testing. By convention, for instance methods like this, I'll put a pound sign in front of the name.
```ruby
describe "conversions" do
  describe '#ounces_to_grams' do

  end
end
```
+ Now, let's write our first test. Here, we'll use a method called `it`. When using `it`, we'll give it a string where we'll describe what the method should do, then in the block we'll actually test it out.
+ First, let's add our expectation:
```ruby
describe "conversions" do
  describe '#ounces_to_grams' do
    it 'given zero, returns 0.0'
  end
end
```
+ Now, if we run RSPEC, we see we have this pending test - so it's a test that's not yet implemented. Some folks will actually write out a bunch of these first and then implement them one at a time.
+ Next, we can test this by actually writing the code, and use a method called `expect` to test that it did what we wanted. I'll show you the syntax for that now:
```ruby
describe "conversions" do
  describe '#ounces_to_grams' do
    it 'given zero, returns 0.0' do
      grams = ounces_to_grams(0)
      expect(grams).to eq(0.0)
    end
  end
end
```
+ So to break this down, we simply call the method and store the return value in a local variable called `grams`. We then use the expect method to say that we expect(grams) to be equal to 0.0
+ If we run this now, we see that the test fails - `undefined method` - this is because our RSpec file doesn't know anything about the file where we define that method. We need to require it - we can do that either in the spec file directly, or in our spec helper. I'll go ahead and include it here directly for now.
```ruby
require_relative '../conversions.rb'

describe "conversions" do
  describe '#ounces_to_grams' do
    it 'given zero, returns 0.0' do
      grams = ounces_to_grams(0)
      expect(grams).to eq(0.0)
    end
  end
end
```
+ Great, and now we see our test passes! A couple of quick configuration options to know about.
+ First, some folks prefer a more verbose output from their tests. I can add an option to my .rspec file to add documentation to the test runs.
```
--require spec_helper
--format documentation
```
+ Running this now - I can see the descriptions I wrote in my describe and it blocks, so that can be nice if you prefer.
+ Finally, as you may or may not be able to tell, by default RSpec displays passing tests in green and failing tests in red.
+ This can be tough for many people to see, as a lot of folks have trouble telling red from green. You can change the color configuration in the `spec_helper` file if you like.
```ruby
RSpec.configure do |config|
  # Adds color configuration
  config.failure_color = :magenta # or whatever color you like
  config.success_color = :cyan

  ## Rest of configuration -
end
```
+ And now those colors will be reflected. So that can be helpful if you want or need to use different colors.

### Using Tests in Learn Labs

+ So we've looked at writing tests. Most of the time though, at Flatiron School, we'll be using tests that someone else wrote to guide our programming.
+ Let's take a look at how we can use the tests to our advantage and what this might look like.
+ I'm going to open up a lab here - this lab is called Methods / Default Values. So let's take a look here.
+ The instructions here say we're meant to define a method that takes in two arguments, and one optional argument.
+ It should print a string to the console describing the meal, and also return that string.
+ Cool, awesome - so let's actually use the test file to guide how we develop.
+ We're going to do a modified version of Test Driven Development, or TDD. Typically in TDD, you write a test, then write just enough code to pass that test.
+ Then you write another test, and change your code so that it passes both tests, and keep going in that fashion until your app does everything it needs to do.
+ In our case, the tests are already written for us, but by solving them one at a time we can follow a bit of the same pattern.
+ So, the first thing I want to do is run `learn` - the `learn` gem that we use actually is just a wrapper for rspec. So it just runs out test suite and then tells learn to make sure our lights turn the right color.
+ We can also run this with an option called `fail-fast` - this means that if we fail one test, our test suite will stop and we'll just see one failure at a time.
+ So let's run that for this lab: `learn --fail-fail`
+ And we see our first test is failing. Let's go ahead and take a look in the spec file:
```ruby
require 'spec_helper'

describe '#meal_choice' do
  it 'should default to meat for the protein' do
    expect(meal_choice("broccoli", "macaroni")).to eq("A plate of meat with broccoli and macaroni.")
  end

  it 'should allow you to set a protein' do
    expect(meal_choice("broccoli", "macaroni", "tofu")).to eq("A plate of tofu with broccoli and macaroni.")
  end

  it 'should puts "What a nutritious meal!" and your order to the console' do
    expect($stdout).to receive(:puts).with("What a nutritious meal!")
    expect($stdout).to receive(:puts).with("A plate of meat with broccoli and macaroni.")
    meal_choice("broccoli", "macaroni")
  end
end
```
+ Looking at the first test, we see that we're calling a method called `meal_choice`, and passing in two arguments. We then expect the output to be this string: "A plate of meat with broccoli and macaroni."
+ If I look at my error message, I see that this method is not defined. I'm going to do the minimum amount of work I need to do fix that error, which is to simply define that method. So in the other file:
```ruby
def meal_choice
end
```
+ When I run the tests again, I don't expect to pass. But I do expect to get a new error message, and that's good, that's progress. Let's run this again using `learn --fail-fast`
+ Cool, so now we see a new error: `Wrong number of arguments - given 2, expected 0` Why do you think that is?
+ Looking at the test, we see that our test is passing two arguments, but our method definition only takes in two. What's the least amount of work I can do to pass this test?
+ Yep, I'll make my method take in two arguments. Some developers, when doing TDD, will actually just use like an underscore for the name.
```ruby
def meal_choice(arg1, arg2)
end
```
+ Cool, so let's run this again now. So now, I see that, my program doesn't throw an error, but the method doesn't do what it's supposed to do. The real easiest way I could get this to work is to simply copy and past that string as the return value.
```ruby
def meal_choice(arg1, arg2)
  "A plate of meat with broccoli and macaroni."
end
```
+ Awesome, and now I see my test is passing green and I'm on to my next failure. The thing is...I don't feel great about the way I'm passing this test. See how this method takes in two arguments? I'm actually ignoring those right now - this meal choice is kind of hard coded right now. So that's not great. So I'm going to do a step called refactoring.
+ Refactoring is when you change how the code does something. So I'm going to make a change, and I expect this method to behave the same way.
+ I'll give names to these arguments - let's call them `veg` and `starch`, then I'll interpolate those values into the string.
```ruby
def meal_choice(veg, starch)
  "A plate of meat with #{veg} and #{starch}."
end
```
+ Cool, and that test still passes. So let's move on to the next test - now, for this one, for also getting a wrong number of arguments error - given three, expected 2.
+ And if I look at the spec, I can see that in this one they're passing in a third argument of "tofu". So now, I'm going to try to fix this test without breaking my first test. So I can't just do this:
```ruby
def meal_choice(veg, starch, protein)
  "A plate of meat with #{veg} and #{starch}."
end
```
+ Because that will break my first test. Instead, I need to make that third argument optional. So I can now use a default value. And that should satisfy both tests.
```ruby
def meal_choice(veg, starch, protein="meat")
  "A plate of #{protein} with #{veg} and #{starch}."
end
```
+ Awesome, so we're passing the first two tests. Reading this next one, there's something new that we haven't seen in rspec yet. But I bet you can guess what this does. Any ideas?
+ So, we're saying - hey, when we call this method, I expect that puts is going to get called, and it's going to get this message. The first message it expects to get is "What a nutritious meal!"
+ So let's add a puts statement to make that test pass
```ruby
def meal_choice(veg, starch, protein="meat")
  puts "What a nutritious meal!"
  "A plate of #{protein} with #{veg} and #{starch}."
end
```
+ Cool, and now we need to puts the second line as well.
```ruby
def meal_choice(veg, starch, protein="meat")
  puts "What a nutritious meal!"
  puts "A plate of #{protein} with #{veg} and #{starch}."
end
```
+ Whoops, and that doesn't work, because now we aren't returning the string. Puts always returns `nil` - so we need to return that string afterwards.
```ruby
def meal_choice(veg, starch, protein="meat")
  puts "What a nutritious meal!"
  puts "A plate of #{protein} with #{veg} and #{starch}."
  return "A plate of #{protein} with #{veg} and #{starch}."
end
```
+ So this works, all of our tests are passing - awesome job! Now, I'm just going to do a bit of refactoring. Ruby actually has implicit returns, so I don't need to use the return keyword here.
```ruby
def meal_choice(veg, starch, protein="meat")
  puts "What a nutritious meal!"
  puts "A plate of #{protein} with #{veg} and #{starch}."
   "A plate of #{protein} with #{veg} and #{starch}."
end
```
+ Run the tests and - yep, still all passing. Great. Now, I don't love that I'm duplicating this string like this, so maybe I'll just make a local variable called `meal` and then I can reference that.
```ruby
def meal_choice(veg, starch, protein="meat")
  meal = "A plate of #{protein} with #{veg} and #{starch}."
  puts "What a nutritious meal!"
  puts
  meal
end
```
+ Awesome, so this works and I feel pretty good about this. So that's it - we've used the specs as our guide and as you can see, they're not too bad. Definitely read them as you are working and use them to help guide you. So to recap what we've learned:

+ We explained the importance of test automation in code - this makes it easy to make changes, and let other developers know that our code works, and also helps us as we're building our apps.
+ We used tests to guide the flow of developing an application - both in a lab and also on our own
+ We explored the RSpec testing environment, including some configuration options, and some of the most useful methods
+ And we used a pre-written test to determine what a method should do or return, and let that guide our development workflow
+ Thanks so much for watching - happy coding!

## Resoruces
+ [Configure RSpec Colors](https://relishapp.com/rspec/rspec-core/v/2-14/docs/formatters/configurable-colors)
