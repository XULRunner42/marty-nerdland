Title: Code Completion with Vim
Author: Kingdon Barrett
Date: Wed Jul 31 2013 03:17:30 GMT-0400 (EDT)
Node: v0.10.15

I've officially begun to cannibalize old blog entries so the list of news on this site does not grow too much larger than the actual amount of information contained within.  This article is about code-completion with go, vim, [YouCompleteMe][], and alternatives.  (The alternatives are, so far, just for go.  YCM is for many languages.)

## Recap

Some useful links I've found on github:

- [YouCompleteMe][]
- [Valloric/YouCompleteMe][]
- [gmarik/vundle][]
- [nsf/gocode][]
- [CoreOS SDK Guide][]

Been working on getting autocompletion set up in vim, but the cool kids said that vim provided by ubuntu is too old.  So, with the recent release of [CoreOS][] to HackerNews, I decided to use that to "dockerize" a vim with the necessary pieces to allow [YouCompleteMe][] to do its job.

[YouCompleteMe]: http://valloric.github.io/YouCompleteMe/
[Valloric/YouCompleteMe]: http://github.com/Valloric/YouCompleteMe/
[gmarik/vundle]: http://github.com/gmarik/vundle/
[nsf/gocode]: http://github.com/nsf/gocode/
[CoreOS SDK Guide]: http://coreos.com/docs/sdk/
[CoreOS]: http://coreos.com/
