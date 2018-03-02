<h2> Intro </h2>
It has been awhile since I have written about my "Adventures in Vim." During my last project I used C# with the Visual Studio IDE. With my newest project, I have been all Vim, all the time. This wasn't a skill I picked up over night, and I will be the first to admit that I am still learning how to use Vim to it's fullest potential. 

For those who are just starting, I would highly recommend using Vim for blog posts to start. Writing blog posts in Vim gave me a simple way to explore navigation in Vim, without worrying about programming language syntax and style.   

In this post I would like to discuss one of the most used Plugins I have, which is NERD tree. I will go over some of the useful keys mappings in NERD tree to get things done.

<h2> What is NERD tree? </h2>
NERD tree is a Vim plugin that allows you to navigate your directories. When you use an IDE, generally you will see a directory tree on the far left side of the window. You can click on directories to open them and find documents you would like to work on. NERD tree gives you the ability to power up Vim so that it resembles other text editors and significantly makes Vim easier to use for larger projects. 

<h2> Helpful NERD tree Mappings </h2>
NERD tree is only as good as your ability to use it. So lets go over the basics of some of the mappings you might want to use in NERD tree.

<h3> Opening Vim </h3>
The most critical thing to know about NERD tree is how to open it. When in Vim, hit `ctrl + n` and you see a window open in the left hand side of the Vim window. You should see a directory of folders based on the directory you opened Vim in. So, for example, if you opened Vim while you were in your Desktop directory, you will see all the files on your Desktop when you open NERD tree.

<h3> Opening Documents in Vim </h3> 
You can navigate NERD tree the same way you navigate Vim using "hjkl" and hitting `enter` to expand directories or `enter` to open a document. Once you open a document, your cursor will move to the open window and leave the NERD tree. Once you leave the NERD tree you can get back to it by hitting `ctrl + w`, which allows you to move from window to window. Now, if you go back to NERD tree and open another ducment it will open in the window that held the previous document you opened. WHAT?! So how do you open multiple windows?

I'm sure you would like to have multiple documents open at once. Well, you can! If you want to open two documents at once, you have options. While in the NERDtree window you can do the following:

`i`.....Open a new horizontal window.
`gi`....Open a new horizontal window with the cursor still in NERDtree.
`s`.....Open a new vertical window.
`gs`....Open a new vertical window with the cursor still in NERDtree.

You can also open multiple windows recursively that are in a directory using `O`. If you wanted to close all thos windows from that directory at once you could use `X`. As you can see, you have plenty of options.

<h3> Editing a Tree </h3>
Lets say you are in Vim and you want to edit your directory by adding additional directories or documents. You could exit Vim and create these things on the command line, or you can use NERD tree, which provides a nice visual way to edit a tree. The mapping `m`, while in NERD tree allows you to manipulate your tree by adding new directories/documents as well as delete or rename them. This gives you a great amount of power over your project. Note that based on where your cursor is when you press `m` you are editing that specific item. 

<h2> Conclusion </h2> 
This post only scrapes the surface of what you can do with NERD tree, but it should be just enough to empower you to let go of your current text editor of choice. For additional help you could always hit `?` when you are in NERD tree to learn more. 
