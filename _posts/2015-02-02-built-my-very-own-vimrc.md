---
title: Built my very own vimrc from scratch
layout: post
published: true
ident: built-my-own-vimrc
---
I've been writing using IDE's since a long time, when I started using linux about 5 years ago, I thought people
who use vim are some crazy people who like to do things the hard way, until one day I decided to read about vim myself,
<!-- more -->
so I looked around and I found a very good book called [a byte of vim][byte-of-vim-link] I recommend it for anyone
who's interested in learning vim, it's free for downloading.  
Anyways since I've read that book I understood why people use it, but I really love IDE's, so I always look for a vim
plugin for all editors I use, like in netbean's jvi and rubymine's ideavim, it's fun, you get the best of the two worlds
vim's fash navigation and editing, and the IDE's smart completion and integrations.


Couple of days ago I decided well why don't I try going pure vim, a lot of people do it, so it might not be as bad as i
think, I tried it couple of times before, but I've always took ready made vimrc files and try it, it always had something
that i didn't like, and because I didn't understand what's really going on in that file I couldn't edit it my self, so
this time i decided to do it manually, from scratch, I got a couple of vimrc's as references and ideas, but I built my own
shortcuts and I got to choose what plugins I want to use and what I don't, I'm very happy with the final result that I
decided to push it to github for history tracking and keeping it from getting lost.


I used an amazing plugin manager called [Vundle][vundle-link], the nice thing about vundle is that it uses github as it's
source, you can simply add any repo path into your vimrc and it would install it and make it available, no need for using
old plugin managers that need updating by maintainers.  
Vundle has only 1 dependency, which is git it self obviously, it's easily installed, you can check the
[quick start][vundle-quick-start] link and you'll find it very easy
I'm gonna include all the sources and my final vimrc, hope it might be of any use to any future users who might want to
try and build their own

Sources:  
  - [Thoughtbot's dot files repo][thoughtbot-dotfiles], and here's the [vimrc][thoughtbot-vimrc]  
  : this vimrc was useful because it had some useful tricks and functions, like changing `<Leader>` which i didn't think
      of before  
  - Swaroop's [vimrc repo][swaroop-vimrc]  
  : it had a lot of bundles to look up and check, some were very useful

Here's my [final vimrc][my-vimrc], always updating it when I want to try something new or undo something

[byte-of-vim-link]: http://www.swaroopch.com/notes/vim/
[vundle-link]: https://github.com/gmarik/Vundle.vim
[vundle-quick-start]: https://github.com/gmarik/Vundle.vim#quick-start
[thoughtbot-vimrc]: https://github.com/thoughtbot/dotfiles/blob/master/vimrc
[thoughtbot-dotfiles]: https://github.com/thoughtbot/dotfiles
[swaroop-vimrc]: https://github.com/swaroopch/dotvim/blob/master/vimrc
[my-vimrc]: http://url.abushady.com/vimrc
