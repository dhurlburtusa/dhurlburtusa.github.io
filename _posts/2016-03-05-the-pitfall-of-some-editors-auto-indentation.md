---
layout: post

doc:
  html:
    head:
      cls: no-js  Doc  Doc--blog  Doc--blog--thePitfallOfSomeEditorsAutoIndentation
      title: The Pitfall of Some Editor's Auto Indentation - Blog - DH

author: Danny Hurlburt
date: 2016-03-05 07:00:00
tags: code indentation pitfall
title: The Pitfall of Some Editor's Auto Indentation
---

Most text editors have smart indentation.  For example, when editing HTML and you press the `Enter` key, the editor
will automatically indent the new line according to the context of the previous line.
<!-- stop excerpt -->
If you started a new tag (a paragraph in the figure below) and then pressed `Enter`, then the editor will indent the
new line one indentation-level deeper than the indentation of the tag.

{% highlight html linenos %}
<body>
    <p>
        <!-- Caret auto-indented to here. -->
    </p>
</body>
{% endhighlight %}

The following is an example of auto-indentation that doesn't hold up well during refactoring.  Here we have a
function named `do_something` that takes many parameters.  Later in the code it is called.  The arguments list
wraps to the next line.  Some editors indent this line depending on the length of the function name.  That is,
the wrapped argument starts at an indentation that lines up with the first argument above.  See the figure
below.

{% highlight python linenos %}
def do_something(param1, param2, param3, param4, param5)
  # ...

do_something(argument1, argument2, argument3, argument4,
             argument5)
{% endhighlight %}

Now consider what happens when the function is renamed.  The arguments will no longer line up.  And there in
lies the pitfall &mdash; extra work to be done when refactoring.

{% highlight python linenos %}
def do_it(param1, param2, param3)
  # ...

do_it(argument1, argument2, argument3, argument4,
             argument5)
{% endhighlight %}

Another approach other editors take is to indent the next line one or two indentation levels.  Notice how `argument5`
is indented by 4 spaces.

{% highlight python linenos %}
def do_something(param1, param2, param3, param4, param5)
  # ...

do_something(argument1, argument2, argument3, argument4,
    argument5)
{% endhighlight %}

When the function is renamed, the indentation-level remains consistent and **predictable**.

{% highlight python linenos %}
def do_it(param1, param2, param3)
  # ...

do_it(argument1, argument2, argument3, argument4,
    argument5)
{% endhighlight %}

For me, this predictability makes reading and comprehending the code easier and I am not slowed down by the
unexpected.

Recall that the indentation depends on the length of the function name.  Now see what happens when functions
with different length names are called.  See how the wrapped arguments are at different indentation-levels.  When
reading, your eyes have to adjust for this unpredictable nature.

{% highlight python linenos %}
def do_something(param1, param2, param3, param4, param5)
  # ...

def do_something_else(param1, param2, param3, param4, param5)
  # ...

do_something(argument1, argument2, argument3, argument4,
             argument5)

do_something_else(argument1, argument2, argument3, argument4,
                  argument5)
{% endhighlight %}

When the code is **predictable**, it is easier to read.  See the figure below.  Compare it with the figure above.
For some people, the difference may be insignificant.  For others, it is a hindrance.

{% highlight python linenos %}
def do_something(param1, param2, param3, param4, param5)
  # ...

def do_something_else(param1, param2, param3, param4, param5)
  # ...

do_something(argument1, argument2, argument3, argument4,
    argument5)

do_something_else(argument1, argument2, argument3, argument4,
    argument5)
{% endhighlight %}

## Summary

I recommend the **predictable** style of indentation.  Code is

* easier to read
* easier to interpret
* easier to comprehend
* resilient to refactoring

when the format is predictable.  When the format is predictable, more brain power can be focused on the meat of the code, and
less brain power is used to parse what is being read.
