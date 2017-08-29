<h2> Intro </h2>
As an apprentice at 8th Light, there are plenty of opportunities to be exposed to a wide variety of tools. Fairly recently I and a few other apprentices were introduced to shell scripting utilizing Bash. I must admit that a great deal of the information went over my head, but I did manage to get my feet wet in the world of shell scripting with Ruby. This may be a surprise to many, but Ruby has the ability to be very powerful on the command line as well as for scripts. I find that because of Ruby's readability it is a great language to learn a wide variety of concepts. For example, I am now writing an unbeatable javascript tic-tac-toe game, and I have found that examples in Ruby have helped my comprehension of the Mini-Max algorithm. Ruby has served as an incredible bridge for difficult concepts, and when I found out that Ruby could be used as a shell scripting tool, I couldn't resist to try.

<h2> Ruby on the Command Line </h2>
When it comes to scripting on the command line lets start with the most basic concept, how to execute a command on the command line:

      $ ruby -e 'puts "Hello World!"'
      Hello World

Using the '-e' command coupled with the 'ruby' call, you can run a wide variety of Ruby. You could also run multiple commands using multiple '-e' commands or a ';' in between commands:

      $ ruby -e 'puts "Hello World!"' -e 'puts "Hi!"'
      Hello World!
      Hi!

      $ ruby -e 'puts "Hello World!"; puts "Hi!"'
      Hello World!
      Hi!

<h3>Reading Files</h3>
Once I was able to do a few simple commands, I looked for ways to read documents. The next useful command I will introduce is 'ARGF' is a stream that can be used for reading STDIN and files passed as arguments. Lets pretend we have a simple text file called 'birthday.txt' that has the following:

      1 Happy Birthday to you,
      2 Happy Birthday to you,
      3 Happy Birthday dear Eric,
      4 Happy Birthday to you!
      5 How Old are you now,
      6 How Old are you now,
      7 How Old are you now,
      8 How Old are you now!

Here I can read a specific line using the following command:

      $ ruby -e 'puts ARGF.readlines[0]' birthday.txt
      Happy Birthday to you,

Now, the first line of the text will be pulled from birthday.txt and displayed. You could also grab the first 'n' amount of lines or last 'n' amount of lines:

      $ruby -e 'puts ARGF.readlines.first(2)' birthday.txt
      Happy Birthday to you,
      Happy Birthday to you,

      $ruby -e 'puts ARGF.readlines.last(5)' birthday.txt
      Happy Birthday to you!
      How Old are you now,
      How Old are you now,
      How Old are you now,
      How Old are you now!

<h3>Computing Word Frequency</h3>
Lets take a deeper dive with our new found skills and see if we can compute the frequency in which a word appears in a given text. Before I do that, let me explain a few new commands. The flag -n is used to loop through your document, line by line, in the style of 'while gets; <your script>; end'. There is also the flag -a which is used to auto split each word found in a line. Then we have the global variable $F, which receives output from the the "split" command. Lets take this knowledge and dissect the following commands:

      $ ruby -n -a -e 'BEGIN { words = Hash.new(0) }' \
      -e '$F.each { |w| words[w] += 1 }' \
      -e 'END { words.select {|k,v| v > 6}.sort_by { |k,v| [-v, k] }.each { |k,v| puts "#{k} - #{v}" } }' \
      birthday.txt

The first command creates a new hash. The next command adds one to each occurrence of a particular word. The last command sorts it in descending order.

The result that should return is:
      you - 7

This is so because in my third command I only wanted words that appeared greater than 6 times.

<h3>Creating a Script</h3>
Now that I had a little know how, I wanted to create my first script using the previous command. The result is as follows:

      1 #!/usr/bin/env ruby
      2
      3 input = ARGV[0]
      4 words = Hash.new(0)
      5 word = File.open( input ){ |f|  f.read.split }
      6 word.each {|w| words[w] += 1 }
      7 words.select {|k,v| v > 2}.sort_by { |k,v| [-v, k] }.each { |k,v| puts "#{k} - #{v}" }

Now, if I wanted to use this script, which I called 'sample_script.rb' I could do the following on the command line:

      $ chmod +x sample_script.rb

This makes the script executable. Then I can run it, with the parameter that I would like to push through in the ARGV array.

      $ sample_script.rb birthday.txt

Simply put, I am calling my script and passing my birthday.txt document as a parameter. The document 'birthday.txt' is passed through and opened in line 5. In the end the script runs, exactly like the previous commands I ran on the command line, but now all I have to do is call my script as opposed to retyping or creating an alias for the previous commands.

<h3>Conclusion</h3>
Shell scripting can be a bit difficult at first, but if you want to create a few commands you can run on the fly and potentially share these scripts with friends and colleagues, I highly recommend shell scripting, especially with Ruby.
