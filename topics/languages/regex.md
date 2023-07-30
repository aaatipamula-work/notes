# Regular Expressions

## Overview

[Regular expressions](https://en.wikipedia.org/wiki/Regular_expression) or more commonly known as regex or regexp is a sequence of characters that that when put together in the proper order creates a match, usually with another string of characters. Regex engines are what do the actual work of matching the text, the sequence of input characters is what directs the engine. It is mostly used in find/replace operations, to parse text and extract values or to validate text.

Good uses of regex may include one of the following:
- Find and replace the string "cat" with "dog" only if the string "wet" precedes the word "cat"
- Only extracting URLs from a large document where the domain name is "google.com"
- Making sure the words in a string are all capitalized.

## Ideas

### Token

A character that holds meaning to a regex engine in that it specifies what text to match. They may vary by the type of engine used but are fairly standard. 

### Matching

REGEX matches strings based on the regex string you feed an engine. Most engines work in a left to right pattern matching characters one at a time *greedily* by default. *Greedy* matching is exactly what it sounds like. The engine matches and "consumes" as many characters as possible when directed to match any number of a character. This behavior can usually be altered to *lazy* match, or match as few characters as possible, by adding a modifier to greedy matching tokens (usually a '?').

### Groups

Most regex engines have the ability to capture certain parts of a match to extract for later use. These are called groups. Grouping is especially useful when extracting certain bits of text that follows or precedes a certain set of text. For example if you were to extract all the URLs in some html but you only wanted urls contained in an `<a>` tag.

## Syntax

The syntax is fairly simple but can be strung together in complex ways. There are varying implementations of regex as well which means you would likely have to look up the syntax for the specific engine that you are using.

That being said here are a few common tokens.

| Token | Meaning |
| --- | --- |
| [abc] | A single character in the bracket "a", "b", or "c" |
| [^abc] | A single character NOT in the bracket "a", "b", or "c" |
| [a-z] | A single character in the range a to z |
| [^a-z] | A single character NOT in the range a to z |
| [a-zA-Z] | A single character in the range a to z or A to Z |
| . | Any single character |
| a\|b | Match 'a' or 'b' | 
| \\s | Any whitespace character (includes tabs and newlines) |
| \\S | Any non-whitespace character |
| \\d | Any digit, equivalent to [0-9] |
| \\D | Any non-digit, equivalent to [^0-9] |
| \\w | Any letter, number or underscore, equivalent to [a-zA-Z0-9_] |
| \\W | Any non-letter, non-number or non-underscore, equivalent to [^a-zA-Z0-9_] |
| (...) | Capture everything enclosed in the parenthesis in a [group](#groups) |
| (:?...) | Match, but do not capture, everything enclosed in the parenthesis |
| a? | Zero or one of 'a'. |
| a* | Zero or more of 'a' |
| a+ | One or one of 'a' |
| a{2} | Exactly two of 'a' |
| a{3,} | Three or more of 'a' |
| a{1,6} | Between one and six of 'a' |
| ^ | The start of a string |
| $ | The end of a string |

*This table was mostly copied from [Regex101](https://regex101.com/)*

**Note**: The tokens `*` and `+` can be modified with the `?` token to be *non-greedy* or *lazy*. 

> e.g. `a*?b` matches zero to any number of 'a' until it reaches a 'b'.

## References

[Regex101](https://regex101.com/) 

- Great for learning and texting your regex with different engines.
