<h2> Intro </h2> 
One aspect of building my server from scratch is that I need my server to pass a test suite known as <a href="https://github.com/8thlight/cob_spec">cob_spec</a>. The implementation of such a task requires some bash scripting as well as the utilization of Git submodules. In this post I will walk through the process that I had to use in order to implement the test suite.

<h2> Git Submodules </h2>
Git submodules setup is pretty straight forward. The <a href"https://git-scm.com/book/en/v2/Git-Tools-Submodules">documentation</a> for Git submodules is written very well with examples. With that, I was able to easily incorporate the cob_spec testing suite into my current project by forking cob_spec first to insure that I wouldn't make any changes to the original cob_spec. Next, I did the following in my root directory of my project, `git submodule add https://github.com/ericdrosado/cob_spec`, where the URL leads directly to my forked repository. The command will clone cob_spec into it's own directory of the same name. Done! Yes, it is that easy. It is important to keep in mind that if you should change anything in this submodule that you will have to make commits separately to your own forked repository. So you'll have to manage both repositories at once.

<h2> Bash Scripting </h2>
According to cob_spec's README, in order to run the test suite you will need to use the following command in it's directory, `java -jar fitnesse.jar -p 9090`. This will run the test suite on `localhost:9090` where you can run the tests. You can also run the tests on the CLI using `java -jar fitnesse.jar -c HttpTestSuite?suite&format=text`.

Now, the reason a bash script was necessary for my project is that I wanted my CI to run both my unit tests as well as the cob_spec acceptance tests. Another added benefit is that I can run both my tests together on the CLI. So, in order to do this I created a script in my root directory named `run_tests`, `touch run_tests.sh`. After this I wrote the following inside my script:
```swift
#!/bin/bash
set -e
swift test
cd cob_spec
mvn package
java -jar fitnesse.jar -c "HttpTestSuite?suite&format=text"
``` 
The first line is what most scripts have to initialize the bash script. It is composed of what's known as the "Shebang" (#!), followed by the path to the interpreter that should be used to run the script. In this case it is the path to Bash.

The next line `set -e` tell the script to exit the script immediately if a command exits with a non-zero status, which would signify an error.

The rest of the script pertains to the commands I would write on the CLI in order to run my tests. The command `swift test` runs my unit tests. The following after that focuses on running cob_spec by entering the correct directory, `cd cob_spec`, and then running maven to download the necessary package components `mvn package`, followed by the command you saw earlier to run the tests, `java -jar fitnesse.jar -c "HttpTestSuite?suite&format=text"`.

<h2> Conclusion </h2>
Bash scripts can do a number of things, such as simplify your life by writing a set of commands that you can execute with a single command or something like in this case, allow your CI to run the necessary commands to run your tests. Honestly, you could do a great deal with these scripts. As I mentioned earlier, now that I have this script I can access it directly and in order to do so I need to allow my script to have executable permissions. You can do this by using the following command `chmod +x /path/to/yourscript.sh` and then you can run your script with the path to your script or a relative path from your root directory. If my script is in my root, I can use the following: `./yourscript.sh`. Ultimately, a great tool to have in your quiver.
