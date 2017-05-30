<h2> Intro: </h2>
  Using RSpec for testing is absoultely amazing for a complete beginner. I've personally dabbled in testing with Java, which was a bit rough, but I have to say that learning RSpec is super straightforward and the way RSpec reads is incredibly beautiful! Besides, reading RSpec in your favorite editor, testing results in the terminal can also read beautifully. The best part, you can customize how your tests look in the terminal through configurations. There is a list of RSpec configurations you can use, but I just want to talk about four of them that I recently learned about from Kevin Skoglund's, "Ruby: Testing with RSpec - Configurations" video.<sup> 1 </sup>

<h2> Configurations in RSpec: </h2>
  The four Configurations that I plan on covering are: 
  1.) Run Tests at Random
  2.) Show Top 10 Slowest Tests
  3.) Find a Single Failure
  4.) Run a Particular Test

  You can set and save these configurations on your computer or you can ship them with code you might push to GitHub. For the purposes of this blog I am just going to show how to call these without saving them locally so you don't have to make any changes to your environment or affect anyones settings in their personal enviornment by forking your code.

  <h3>Run Tests at Random</h3>
    In order to run tests at random you can traverse to the directory that is holding your .rspec file that you initiated. Once there you can run the command:

    rspec --order random 

    This will run all your tests at random. Why would this be helpful? Well, lets say you have many tests and you want to insure that their order doesn't play a role on whether or not they pass or fail, that would make this tool helpful.<sup> 1 </sup>

  <h3>Show Top 10 Slowest Tests</h3>
    In order to show the top 10 slowest tests you can once again traverse to the directory that is holding your .rspec file that you initiated. Once there you can run the command:

    rspec --profile

    This will obviously give you a list of your top 10 slowest tests. If there is one thing I have learned is that tests should be fast! <sup> 2 </sup> Tests should be fast so that you run them and run them often, whereas if you have very slow tests, you are less likely to run them all. Sometimes it is good to go back and see what you can do to allow your tests to run faster.

  <h3>Find a Single Failure</h3>
    In order to find a single failure you can once again traverse to the directory that is holding your .rspec file that you initiated. Once there you can run the command: \n

    rspec --fail-fast

    This will quickly run and find a single failure. This is helpful if you have many tests and you just want to deal with them one at a time. Really nothing more to it...moving on. \n

  <h3>Run a particular test</h3>
    Now, here is a tool you may come to love as much as I have. When it comes to trouble shooting sometimes you just need to test a specific test where this little one comes in handy. You can do this by typing in the name of the rspec file followed by the first line your test is on. In order to do this you need to be in the directory where your test file is or you can write out the path. Here is an example of a rspec file called "car_spec" while already traversing into the spec directory:

    rspec car_spec.rb:7

    Notice the rspec call, then the file name, followed by the line number after the colon. Once again, a great way to test a specific test in your long list of tests.


<sup> 1 </sup> Skoglund, Kevin. (2015, February 5). www.Lynda.com - Ruby: Testing with RSpec: Configuration .Retrieved from https://www.lynda.com/Ruby-tutorials/Configuration/183884/371434-4.html \n
<sup> 2 </sup> Haines, Corey. (2014, June 4). "Four Rules of Simple Design". LeanuPub Publishing 2014