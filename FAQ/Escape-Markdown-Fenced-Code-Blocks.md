If you're writing developer documentation that includes occasional markdown snippets that also recursively contain fenced code blocks that shouldn't be expanded but displayed as raw markdown, you might be scratching your head how to escape a fenced code block inside of the hosting code block so that it doesn't render the code snippet as code.

### Escaping the Escape
It turns out Markdown has a way to escape code fencing using special character combinations:

* `~~~`
* `` ```` ``

To escape a fenced code block you can use the following:

````markdown
~~~
The text below is **not expanded**:

```cs
int x = 100;
```
~~~
````

You can use either `~~~` or 4 backticks.

And... to make things even more interesting... you can nest the escaped fence into yet another level of escaped fencing by using the other escape sequence of the two giving you 3 level of escapes. The display here in fact does this so I can display the two levels of non-escaping.

### Escaping BackTicks in Inline Code Blocks
You can also escape backticks in inline code blocks by using double backticks for the code delimiter.

If you wanted to delimit **List``** you can use:

````markdown
``List`1``
````

To delimit a single backtick:

````markdown
`` ` ``
````

which produces: `` ` ``

Notice the extra spacing - this is necessary only if you start or end with a backtick.

To display triple ticks:

````markdown
`` ``` ``
````

which produces: `` ``` ``

Not pretty but  if you have to do it this is quite the life saver.