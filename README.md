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

+ This is our first intro to automated testing - and naturally this test is a bit hard to read.
+ Use a library called rspec
+ Demo install rspec, make an app_spec file and write a simple test in it.
+ Open a lab, open up the test file
+ Read the tests - explain describe and it
+ Show running and seeing the failure - we can use the errors to guide us
+ Show running with fail-fast to see only one error at a time
+ Show that you should only fix that one particular error - do the minimum amount of work possible
