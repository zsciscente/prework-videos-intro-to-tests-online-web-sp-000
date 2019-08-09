# Intro to Tests

## Learning Goals
+ Explore the RSpec testing environment
+ Explain the importance of test automation in code
+ Use tests to guide the flow of developing an application
+ Use a pre-written test to determine what a method should do or return
+ Predict what error message a test will throw when executed 
+ Use the `fail-fast` flag with rspec tests

## Outline
+ Start with overview: will look at automated test suites, why they're important, and how to use the test suite for learn labs.
+ When we build applications - we usually define some methods or code, then run it someplace else. A lot of apps will have a bunch of files that define things, then other files to use what was defined.
+ Here's a method that converts ounces to grams
  + How might we test this? 
  + We could call the method in IRB and try some stuff out
  + If we change this later, won't have documentation on what this method should do
+ So let's actually make a file that we can run that will test this method for us, and let us run it in case anything changes
  + `touch`app_test.rb`
+ Write a simple statment to check the answer and see if the test failed or not
```
require_relative './app.rb'

puts "Given 1, it should return 28.3495"
answer = ounces_to_grams(1)
if answer == 28.3495
  puts "Passed!"
else
  puts "Test failed: got #{answer} instead"
end
``` 
+ This is our first intro to automated testing - this test file is a bit hard to read. 
+ Use a library called rspec
+ Demo install rspec, make an app_spec file and write a simple test in it. 
+ Open a lab, open up the test file
+ Read the tests - explain describe and it
+ Show running and seeing the failure - we can use the errors to guide us
+ Show running with fail-fast to see only one error at a time
+ Show that you should only fix that one particular error - do the minimum amount of work possible
