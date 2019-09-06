# Intro to Tests

## Learning Goals
+ Explain the importance of test automation in code
+ Use tests to guide the flow of developing an application
+ Explore the RSpec testing environment
+ Use a pre-written test to determine what a method should do or return
+ Predict what error message a test will throw when executed

## Lesson
+ Hi folks, this is Ian from Flatiron School. In this video, we're going to look at Testing and Test Driven Development.
+ Our learning goals for this video:
  + We'll explain the importance of test automation in code
  + We will use tests to guide the flow of developing an application
  + We'll explore the RSpec testing environment
  + Also we'll use a pre-written test to determine what a method should do or return
  + And we'll try to predict what error message a test will throw when executed
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
+ And now those colors will be reflected.

### Using Tests in Learn Labs
+ Open a lab, open up the test file
+ Read the tests - explain describe and it
+ Show running and seeing the failure - we can use the errors to guide us
+ Show running with fail-fast to see only one error at a time

## Resoruces
+ [Configure RSpec Colors](https://relishapp.com/rspec/rspec-core/v/2-14/docs/formatters/configurable-colors)
