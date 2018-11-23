# Kakoune (dpc's fork)

`kakoune-dpc` is my personal fork of Kakoune.

Most probably you want to go to the original project:

* http://kakoune.org
* https://github.com/mawww/kakoune/

**Please open issues only related to the forked part.**

## Why fork?

I really enjoy Kakoune, I invested quite a bit of time to switch to it
and get use to it. It gets a lot of stuff right.

But **I can't stand the way `x`/`X` keys work**! They work consistently
in theory, but inconsitently in practice.

The room of the problem is that Kakoune can not make a distinction between
an empty line, and fully selected line. So if you want to eg. delete
a current line, you have to pay attention if it's empty or not. Which is driving 
me crazy!

The way I see it, Kakoune prides itself in
[stuff like VimGolf](https://delapouite.github.io/kakoune-tv/), but in my
opinion it doesn't matter how many keystrokes do you need to get something done,
only how quickly can you type them with confidence and without mistakes!

Visual selection of Kakoune improves everything most of the time, but behavior
of `x` is screwing everything up, because you have to constantly look at
content of the buffer to do things as simple as reliably selecte a line. You
loose your speed, so what's the point? In Vim you could at least reliably push
`dd` and be done with it.


```
typing without looking (this fork) > visual feedback (original Kakoune) > no feedback (Vim)
```

Helpful Kakoune community ofered mostly band-aids of eg. using `<a-x>`, which in my
opinion are unsatisfying. If I wanted to push alt and control all the time,
I would be using Emacs. 😂

That's why I took a liberty given by Open Source, and the fact that Kakoune codebase
is nice and easy to understand, forked and changed the behavior of
`x`-and alikes. Now pressing `x`/`X` the first time always selects the current
line, and only selects next line when pressed consecutively.

You can look for more details here:

* Discussion: https://github.com/mawww/kakoune/issues/2590
* PR: https://github.com/mawww/kakoune/pull/2595


### Demo

Watch the recording:

https://asciinema.org/a/213671


### Details

I've split my changes into following branches:

* `line_editing` - this branch changes `x` and `X` to work in a predictable
  fashion, by tracking if they were pressed consecutively.
* `line_editing_with_highlight` - the above plus a visual feedback
* `line_editing_ext` - all the above plus `<a-x>`, `<a-X>` and `J`, `K`, `L`, `H`
  were changed to act a bit differently, basically introducing a full-featured
  "line selection sub-mode"
* `master` - like `line_editing_ext` plus branding to explain this is a fork


You can read the commit log for a better idea what each change does exactly.

### What about misbehaving plugins

If it becomes a problem, please report it, and I'll introduce a fix so that
"line editing sub-mode" behavior changes happen only when typing interactively from
the terminal. This way plugins can depend on the original behavior, and
users can have the candy.
