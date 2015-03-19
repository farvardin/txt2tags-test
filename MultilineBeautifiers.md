# Multiline Beautifiers #

Since day zero, all txt2tags beautifiers are only valid if opened and closed on the same line:

```
Hello, **this is bold**.

But **this
is not**.
```

Some users have asked for multiline beautifiers, so you can open bold (or italic, underline, strike) in one line and close it in another line. This would make both previous bold examples to work.

# Problems #

For years, users rely on oneline beautifiers. If we change that, some false positives may appear. See an example where a false `--strike out--` mark would be recognized:

```
Do you prefer --i or
i-- to decrease your counter?
```

URLs are also specially tricky, since the double // can be confused with italic marks. In oneline beautifiers you just break the line to avoid confusion. In multiline the program needs to be smarter.

```
Please visit http://foo.com
and http://bar.com.
```

And what about cross-paragraph beautifiers? Should we support it? The targets do support it? Complexity increases.

```
I want to open **bold here.

But I'll only close it
here.**
```

If we support it, then false positives such as the previous strike out and italic examples would be even harder to recognize since the opening and closing tags could be pages away one from each other. Even harder if the target doesn't support the specific beautifier, then only the false marks will disappear. The first example in the Man Page target will give:

```
Do you prefer i or
i to decrease your counter?
```

And not closed marks? They're marks or just common text?

```
To access products data, use the **products pointer.
```

# Ideas #

An specific mark for beautified blocks. Using the already consistent three-symbols-for-blocks syntax, we could have:

```
***
This is a bold paragraph.
Intuitive marks, ain't it?
***
```

But once again, the problem of cross-paragraph marks will appear:

```
***
First paragraph.

Second paragraph.

- Maybe a list here?
- Things are getting strange.
-

Oh, I need to close the bold block.
***
```

And things get specially tricky if we mix beautifier blocks, messing the nesting hierarchy:

```
***
This is a bold paragraph.

///
Now an italic one.
Oh, and bold also,
since we didn't close it.

___
***
Underlined paragraph, anyone?
Bold was closed, but italic not.

///
---
Now I closed italic.
But opened a strike out paragraph.
And... underlined is still opened (I guess).
Hey, I'm lost.
```

We can restrain the bold/italic/underline/strike block to automatically close we the paragraph has ended. But that's a strange limitation that make me think not implementing beautifier blocks is the best solution.

```
***
This is a bold paragraph.

The second paragraph is not bold anymore.
The bold was automatically closed.
```

The same kind of problems with cross-paragraph and auto-closing will appear for other syntax ideas, since the concept is the same:

```
We can use **the current
mark.**

Or invent a ***new mark
specially for multiline
beautifiers*** inside a
paragraph.

Or invent some kind of
%%b1 bold macro that can
be turned ON and OFF. %%b0

Or...
```

And don't forget that the "cross-paragraph problem" can also be expanded to cross-any-block-structure, such as quotes, lists, titles, tables...

```
I'm feeling **bold today.

| My nice | table |

I'm still bold?
```

# Conclusion #

Multiline beautifiers are tricky by nature.

We need very consistent and strong rules to add them, to avoid all these problems.

That's why txt2tags prefers the oneline beautifiers feature.

Please leave a comment to share your ideas on this topic!