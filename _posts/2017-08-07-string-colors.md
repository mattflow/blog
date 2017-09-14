---
layout: post
title:  "String Colors"
subtitle: "Every string should feel special, so I gave each one its own color."
date:   2017-08-07 14:48:00 -0400
author: "Matt Flowers"
header-img: "assets/img/string-colors-header.jpeg"
comments: true
---

This idea came to me when I was making a list application for my parents to make
it easier for them to keep track of different things (mainly groceries). The app's
main screen is a grid view of all the different lists created. Instead of having
each tile have an image associated with it, I decided to keep it simple and use
colored tiles.

So I came up with the idea to hash the name of the list into a unique, hexadecimal
color code.

Growing up in the age of the interenet is a real double edged sword. You have free
access to an insane amount of information. The down side is that it is almost impossible
for a computer science student to research something and attempt to figure it
out on their own (thanks a lot, Stack Overflow).

Five minutes into hashing algorithm research and I cam across a Stack Overflow
article explaining exactly how to do what I was looking for. Since I am still
interested in the subject of hashing, I decided to break down and understand
the code line by line.

The first part of the journey starts with hashing the string.

```js
function hashCode(str) {
  var hash = 0, chr;
  for (var i = 0; i < str.length; i++) {
    chr   = str.charCodeAt(i);
    hash  = ((hash << 5) - hash) + chr;
    hash |= 0;
  }
  return hash;
}
```

Now this code block is pretty straight forward, so I think we can jump right into
the loop (which is simply iterating over the characters in a string).
The `hash` is being set to the previous `hash` shifted 5 bits left. The reason
for the five bit shift is because a left bit shift is equal to multiplying by 2,
so `((hash << 5) - hash) == hash * 31`. Shifting bits require less multiplications,
so it is faster than simply multiplying by 31. We use the number 31 because
it is a prime number and those are traditionally suggested when it comes to hashing.
The next character code is then added onto that hash. the final
line, `hash |= 0` is just there to convert the hash into a 32 bit integer. This is because
the bitwise OR operator runs a bitwise OR operation on each bit of the two
operands and sets the results in the hash. This makes sure that the hash is now 
a 32 bit integer.

```js
function colorCode(hash) {
  var c = (hash & 0x00FFFFFF)
    .toString(16)
    .toUpperCase();
  return '#' + ('00000'.substring(0, 6 - c.length) + c);
}
```

This function takes the 32 bit integer hash that was computed in the previous 
function and converts it into its hexadecimal representation. It then turns that
hex number into a uppercase string and formats it as a valid color code.

That leaves you with a color code that is unique to the string that you typed in.
This has algorithm has a very low chance of collisions.

Keep in mind that this hash is meant to return a UNIQUE color, not a random one.
Because of this, some similar words might have similar colors. Also, the longer
the word/phrase, the more scrambled the hash will become.

You can demo my string color webpage [here](https://mattflow.github.io/string-color).

There is currently a bug in chrome that makes an off-color square appear behind
the input box. If that is bothering you, I would try using another browser or even
try it on mobile!