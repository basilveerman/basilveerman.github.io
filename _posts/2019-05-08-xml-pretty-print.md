---
layout: post
title: Pretty printing xml
---

A large portion of my day is spent in a command line environment. When inspecting data, I use many different tools to help in this: `grep`, `less`, `find`, `sort`, `cut`, etc. If I'm looking at json data, this normally comes from some source that delivers this as a single long string. Python's `json.tool` comes to the rescue to convert this wall of text into prettified and human redable data. Here is the example from the (docs)[https://docs.python.org/3/library/json.html#module-json.tool]:

```bash
$ echo '{"json":"obj"}' | python -m json.tool

{
    "json": "obj"
}
```

OK, so that's great! What if that terrible day arrives and you want to look at unformatted *xml* data in a command line environment? You _could_ just use `xmllint`, but that would just be too easy and remove the reason for writing this post.

```bash
$ echo '<data><country name="Liechtenstein"><rank>1</rank><year>2008</year><gdppc>141100</gdppc><neighbor name="Austria" direction="E"/><neighbor name="Switzerland" direction="W"/></country></data>' \
| python -c "import sys; from xml.dom import minidom; print minidom.parseString(sys.stdin.read()).toprettyxml()"

<?xml version="1.0" ?>
<data>
    <country name="Liechtenstein">
        <rank>1</rank>
        <year>2008</year>
        <gdppc>141100</gdppc>
        <neighbor direction="E" name="Austria"/>
        <neighbor direction="W" name="Switzerland"/>
    </country>
</data>
```

Huzzah! It works! While this quick snippet was fun to write, I'll probably never use it.

From _The Zen of Python_:
<pre>
	Simple is better than complex
	There should be one-- and preferably only one --obvious way to do it.
</pre>

In this case, I'd argue for the simple and obvious choice of _not_ using python for this task.
