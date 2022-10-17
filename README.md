# PRO Regex Tutorial

This tutorial is designed to highlight the different ways that Regular Expressions (Regex) allow you to search through, validate, and replace text.

## Summary

In this tutorial we will examine the following regex:

```/(?:(\+\d)[ -])?\(?(?<areacode>\d{3})\)?[ -]?(\d{3})[ -]?(?<lastFour>\d{4})/gm```

This Regex searches for a match of the various valid forms of phone numbers that are commonly used.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)
- [Resources](#resources)

## Regex Components

### Anchors

There exist the following Anchors:

| Anchor      | Description                       |
| ----------- | --------------------------------- |
| ^           | Match the beginning of the text   |
| $           | Match the end of the text         |
 
Our Regexegex expression does not use any anchors.


### Quantifiers

There exist following Quantifiers:

| Quantifier  | Description                |
| ------------| -------------------------- |
| *           | Match zero or more times   |
| +           | Match one or more times    |
| ?           | Match zero or one times    |
| { n }       | Match exactly n times      |
| { n ,}      | Match at least n times     |
| { n , m }   | Match from n to m times    |

Quantifiers used in our regex expression:

| Quantifier   | Description                                 |
| ------------ | ------------------------------------------- |
| (?           | May or may not include open parenthesis     |
| )?           | May or may not include closed parenthesis   |
| [ -]?        | May or may not include a space or hyphen    |


### OR Operator

In a regular expression, an OR Operator is denoted with a vertical line character | .    
Alternation allows any expressions.    
Ex:    

```A|B|C```    

means either    

```A, B or C```    

Our Regex expression does not use any OR Operators.


### Character Classes

There exist following Character Classes:    

| Class  | Description                                            |
| -------| ------------------------------------------------------ |
| /d     | Numbers                                                |
| /D     | Any character except numbers                           |
| /s     | Space symbols, tabs, newlines                          |
| /S     | Anything other than space symbols, tabs, newlines      |
| /w     | Latin letters, numbers, underscore                     |
| /W     | Anything other than Latin letters, numbers, underscore |
| .      | any character except line breaks                       |

Our Regex uses the following Character Classes:

| Class  | Description                                            |
| -------| ------------------------------------------------------ |
| /d     | Numbers                                                |


### Flags

There exist the following Flags:    

| Flag | Description                                                                  |
| ---- | ---------------------------------------------------------------------------- |
| i    | Search is case-insensitive: no difference between upper and lower case       |
| g    | Search looks for all matches, without it – only the first match is returned  |
| m    | Handles an input string that consists of multiple lines. Affects ^ and $ anchors so they match the beginning and end of a line, instead of just an input string |
| s    | Enables “dotall” mode, that allows a dot . to match newline character      |
| u    | full Unicode support. The flag enables correct processing of surrogate pairs (includes 4-byte characters)   |
| y    | “Sticky” mode: searching at the exact position in the text (used for performance gain - only checks one positiopn rather than all text)   |

Our Regex uses the following flags:

| Flag | Description                                                                  |
| ---- | ---------------------------------------------------------------------------- |
| g    | Search looks for all matches, without it – only the first match is returned  |
| m    | In this case we are using the m flag to search multiple numbers on multiple lines |


### Grouping and Capturing

Regular expressions can also be used to extract information for further processing. This is done by defining groups of characters and capturing them using parenthesis (). Any subpattern inside a pair of parentheses will be captured as a group. The group can be also be labeled within brackets <label> to simplify further processing.

Our Regex uses the following Grouping/Capturing:

| Grouping/Capturing | Description     |
| ---- | ----------------------------- |
| ```(\+\d)```  | This grouping includes the country code
| ```(?:(\+\d)[ -])```  | By using the ```(?:)``` around ```(\+\d)``` we are excluding the space that may come after the country code  |
| ```(?<areacode>\d{3})```  | This grouping includes the area code and is labeled as such
| ```(\d{3})```  | This grouping includes the first three digits of a phone number
| ```(?<last-four-digits>\d{4})```  | This grouping includes the last four digits of a phone number and is labeled as such

By using the groupings in our Regex we can capture and output these different forms of phone numbers all in the same format:

Using the Groupings we can search:    
```$1$2$3$4```

| Numbers          | Captured Output    |
| ---------------- | -------------------|
| 1234567890       | 1234567890         |
| 123-456-7890     | 1234567890         |
| 123 456 7890     | 1234567890         |
| (123) 456-7890   | 1234567890         |
| +1 123 456 7890  | 1234567890         |


### Bracket Expressions

Brackets [] indicate a set of characters to match. Any individual character between the brackets will match, and you can also use a hyphen to define a set.

Our Regex uses the following Brackets:

| Brackets | Description        |
| ---- | ----------------------- |
| ```[ -]```    | In this case the Brackets are saying that either a space or a hyphen will match  |


### Greedy and Lazy Match

| Quantifier Operation Modes | Description     |
| ----------------- | ----------------------------- |
| Greedy | MATCH AS MANY repetitions of the quantified pattern as possible. By default quantifiers are greedy (+)
| Lazy | MATCH AS FEW repetitions of the quantified pattern as possible. A regular quantifier is made lazy by appending a ? question mark to it. |

Our Regex does not use quantifiers.

### Boundaries

A word boundary \b is a test, just like ^ and $.

When the regexp engine (program module that implements searching for regexps) comes across \b, it checks that the position in the string is a word boundary.    
There are three different positions that qualify as word boundaries.    
At string start, if the first string character is a word character \w.    
Between two characters in the string, where one is a word character \w and the other is not.    
At string end, if the last string character is a word character \w.

There are no boundaries in our Regex.


### Back-references

 Back-references refer to a previous part of the matched regular expression. They are specified with a backslash and a single digit that represents the group number (e.g. "\1"). They can also be referened by the name given to the group:    
 ```\k<areacode>``` would reference this group in our regex ```(?<areacode>\d{3})```    
 The part of the regular expression they refer to is called a subexpression, and is designated with parentheses. Back-references are used to match the same content as a previously matched subexpression.

 Our Regex does not use any back-references.


### Look-ahead and Look-behind

Look-ahead and Look-behind (Lookarounds) are used when we need to find only those matches for a pattern that are followed or preceded by another pattern.

There exist the following types of lookarounds:

|   Pattern    |	   Type	            |      Matches            |
| X(?=Y)	   |  Positive lookahead	| X if followed by Y      |
| X(?!Y)	   |  Negative lookahead	| X if not followed by Y  |
| (?<=Y)X	   |  Positive lookbehind	| X if after Y            |
| (?<!Y)X      |  Negative lookbehind	| X if not after Y        |

Our Regex does not use any lookarounds.


## Resources

- [javascript.info](https://javascript.info/regexp)    
- [regexr.com](https://javascript.info/regexp)    


## Author

[colinmichael89@gmail.com](mailto:colinmichael89@gmail.com). View more of my work in GitHub at [colinmichael89](https://github.com/colinmichael89)
