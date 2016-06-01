---
published: true
title: Having fun with the developer console
layout: post
---
I've been working as a web developer for many years now. It's one of those areas where you can't possibly know everything (if you claim to, you are wrong) - there is just too much going on, and its constantly changing or being added to.

But this isn't always a bad thing. Sometimes you come across something new, which changes how you work, and that you wished you'd known about for years - a "light-bulb" moment, and its hugely rewarding to find new ways to improve your work.

The Chrome developer console is a fun example of this; It contains a number of secrets that I never even knew existed, and pretty much blew my mind when I found out about them (note: I'm pretty sure the Firefox developer console also supports this, and possible other browsers, though I haven't checked. Remember to be careful with console statements in IE&lt;10, as they only work with the console window open - otherwise they throw error messages - thanks again, Microsoft).

Everyone knows about console.log, right? It allows a user to write a message to the browser console from their code. Here's an example:

    console.log(obj);

![Console.log example](/_images/consolelog.png)


## console.table is awesome
But did you know about console.table? I certainly didn't. Console.table allows you to pretty print variables (arrays and objects) in a readable, sortable table.

    console.table(obj.items);

![Console.table example](/_images/consoletable.png)


You can EVEN filter the table further by providing an array of field names as a second parameter in the statement:

    console.table(obj.items,["field1","field3"]);

![Console.table example 2](/_images/consoletable2.png)

Pretty neat huh? Since I've worked heavily recently with JSON API's and part of the information I've been trawling through was to check data to make sure the system was outputting the correct fields, this would have been VERY handy indeed. Hindsight - its a wonderful thing.

## Wait, there is more..
It doesn't stop at console.table. There are a bunch of other useful console functions that go sadly underused:

console.info - like console.log but highlights with a little exclamation mark

    console.info("We're nearly there.")

![Console.info example](/_images/consoleinfo.png)


console.error - throws a custom js error message to the console

    console.error("SOMETHING WENT WRONG");

![Console.error example](/_images/consoleerror.png)


console.warn - throws a js warning message to the console

    console.error("SOMETHING WENT WRONG");

![Console.warn example](/_images/consolewarn.png)


console.debug - throws a debugging message to the console

    console.debug("Whats going on?");

![Console.debug example](/_images/consoledebug.png)


console.group - console.groupEnd - This allows you to group together a bunch of console.log messages into a "group", like a collapsible accordion of console messages.

    console.group("group1");
    console.log("hi");
    console.log("google");
    console.groupEnd();

![Console.group example](/_images/consolegroup.png)


console.time - console.timeEnd - this allows you to time a certain set of instructions and output how long they took. You pass a unique string to identify the timer

    console.time("test");
    setTimeout(function(){
      console.timeEnd("test");
    },1500);

![Console.time example](/_images/consoletime.png)


I've created a codepen filled with the examples I've talked about above. Find it below, and feel free to play around. Hopefully at least some of these will give you the same "light-bulb" moment they gave me:

[http://codepen.io/ctaylr/pen/GqRVXe]()
