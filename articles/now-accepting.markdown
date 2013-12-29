Title: Code Completion with Vim
Author: Kingdon Barrett
Date: Wed Jul 31 2013 03:17:30 GMT-0400 (EDT)
Node: v0.10.15

This article is about code-completion with go, vim, [YouCompleteMe][], and
alternatives.  (The alternatives are, so far, just for go.  YCM is for many
languages.)

## Update

It works!

- [u/yebyen/vim][]: My Docker Repo

If you've built CoreOS, or if you got docker another way, you can enjoy my
code-completing setup in a container without going through the trouble of
setting it up for yourself :) visit [my Docker Index page][]'s one lonely
repository, `yebyen/vim`, and start reading at around *Full Description*.

Or, check out [initial setup][] and see what I've done to the already existing
basic [tianon/debian][]`:jessie` to make this bundle of joy from a truly
spartan debian base image.  I've tried to capture everything in the gist but
there are some pieces missing, namely, fumbling around to configure omnifunc
and YouCompleteMe's python configuration -- this is all done in `latest` tag.

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
[u/yebyen/vim]: https://index.docker.io/u/yebyen/vim/
[my Docker Index page]: https://index.docker.io/u/yebyen/
[initial setup]: https://gist.github.com/kingdonb/39d777da7d44a376fedd
[tianon/debian]: https://index.docker.io/u/tianon/debian/
