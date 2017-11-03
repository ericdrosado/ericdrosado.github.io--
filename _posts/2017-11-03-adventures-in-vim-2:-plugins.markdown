<h2> Intro </h2> 
To recap, in my last blog post I discussed my initial impressions of Vim and where to start to learn the Vim basics. Now it is time to explore the never ending power that is Vim plugins! 

Vim Plugins allow you to customize certain aspects of your Vim environment. In this post, I would like to go step by step on how to store vim plugins using .vimrc, which is a script that holds your Vim preferences, and Vundle, your first plugin.

<h2> Setting up your .vim and .vimrc Directories</h2> 
In your root user directory you may already have a ".vim" file. In order to check, on the command line use the ```$ cd ~``` command to go to your user home directory and then type ```$ ls -a``` and you will be given a list of files and directories. If you see ".vim" go ahead and open that directory. If you do not see that directory you need to create it using the following command in the user home directory ```$ mkdir .vim```. 

Once in the .vim directory you want to make a ".vimrc" file using the command ```$ touch .vimrc```.

<h2> Setting up Vundle </h2>
I am introducing Vundle as your first plugin, because it is a plugin manager. This will allow you to add plugins easily in the future.

You will have to clone Vundle from a git repository in order to use it. In order to do this you will use the following command on the command line, which will direct Vundle to load in your .vim directory: ```$ git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim```.

Now we need to configure Vundle in your .vimrc file. Go ahead and open your .vimrc file in your favorite text editor of choice, which as this point should be Vim.In your .vimrc file you want to paste the following:
```
set nocompatible              " be iMproved, required
filetype off                  " required

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'

" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required
" To ignore plugin indent changes, instead use:
"filetype plugin on
"
" Brief help
" :PluginList       - lists configured plugins
" :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ
" Put your non-Plugin stuff after this line
```  
Now, there is a lot here, but Vundle has taken the opportunity to explain a good portion following the open quotations ("). The Vundle documentation is pretty clear, but I want to point you to one of the most important pieces here to add plugins. Between ```call vundle#begin()```and  ```call vundle#end()``` is where you will add your plugins. There are a few supported formats to add plugins, but if you look at how the Vundle Plugin is added, ```Plugin 'VundleVim/Vundle.vim'```, you will notice in order to add plugins you can find the github repo and use the format "USER/REPO_NAME" to add them to your running list. That is it! MAGIC!

<h2> Conclusion </h2>
Plugins will make your life much easier when it comes to using Vim. I would recommend also obtaining the NerdTree plugin for Vim to view a tree of your files and directories when you are working on a project. As I come about new tools, I will continue to add more resources on this blog. 
