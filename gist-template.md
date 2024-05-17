# Youtube URL Regex

a regex explaining the use of a youtube URL Id grabber.

## Summary

This regex is able to call any youtube video URL and grabs the id:

/ (?:https?:)?(?:\/\/)?(?:[0-9A-Z-]+\.)?(?:youtu\.be\/|youtube(?:-nocookie)?\.com\S*?[^\w\s-])([\w-]{11})(?=[^\w-]|$)(?![?=&+%\w.-]*(?:['"][^<>]*>|<\/a>))[?=&+%\w.-]* /

This regular expression extracts the 11-character video ID from various YouTube URL formats while ensuring it's properly delimited and avoiding matching within HTML tags or query parameters. In this tutorial I will break down what each component does and how it can be used in context.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

there are several important parts to this regex that can be broken down into understandable elements.

(?:https?:)
(?:\/\/)
(?:[0-9A-Z-]+\.)
(?:youtu\.be\/|youtube(?:-nocookie)
\.com\S*
[^\w\s-])([\w-]{11})
(?=[^\w-]|$)
(?![?=&+%\w.-]
*(?:['"][^<>]*>|<\/a>))
[?=&+%\w.-]*

### Anchors

the two principal anchors of thus regex are the Positive Lookahead (?= ... ), and the Negative Lookahead (?![ ... ]). In the positive lookahead a zero-width assertion is placed, that specifies a pattern to match without consuming characters. In this regex, (?=[^\w-]|$) is a positive lookahead that ensures that the match for the video ID is followed by either a character that is not a word character or a hyphen, or it's the end of the string ($). This prevents matching partial IDs or IDs within larger strings.

For the negative lookahead it has similar aspects that have a zero width assertion but it specifies a pattern that should not be present after the current position in the string. In this  part of the regex: (?![?=&+%\w.-]*(?:['"][^<>]*>|<\/a>)) is a negative lookahead that ensures that the match for the video ID does not occur within certain sequences of characters, like the HTML tags or query parameters. This prevents matching IDs that are part of a larger URL or surrounded by unwanted characters.

### Quantifiers

the question marks spiting the URL are quantifiers that make the preceding element optional. It matches zero or one occurrence of the preceding element. For example, (?:https?:)? makes the "http://" or "https://" part of the URL optional.

the all symbol or star icon '*' is given in specific places of the regex like: [?=&+%\w.-]* matches zero or more occurrences of characters that could be part of query parameters or special characters in the URL.

### Grouping Constructs

first the non capturing groups are '(?:\/\/)?', '(?:https?:)?' These are used for grouping without capturing the matched text. They are useful for defining optional parts of the regex without affecting the overall capture groups.

next is the capturing group: '([\w-]{11})' this captures exactly 11 word characters or hyphens (the YouTube video ID) and stores it as a separate capture group. It's used to capture the matched text so that it can be referenced later.

### Character Classes

these Character classes '[0-9A-Z-]', '[\w-]' are used to match any single character from a set of characters.

### The OR Operator

The '|' is used to show the alternatives. It allows the regex engine to match either of the specified alternatives. In '(?:youtu\.be\/|youtube(?:-nocookie)?\.com\S*?[^\w\s-])' the OR is matching different formats of YouTube URLs. 'youtu\.be\/' Matches the shortened "youtu.be/" URL. While 'youtube(?:-nocookie)?\.com\S*?[^\w\s-]' This part matches the full "youtube.com" URL with optional "-nocookie" parameter and any additional characters that are not word characters, spaces, or hyphens. The '|' operator separates these two alternatives, allowing the regex to match either the shortened URL format or the full URL format

### Character Escapes

The '\.' is a literal period (.). The backslash (\) is used to escape the period because in regex, a period typically represents any character except newline. the '\w' and the \W symbols represent any word character, and any non-word character respectively, which includes alphanumeric characters and underscores. '\s' Is any whitespace character, including spaces, tabs, and newlines and finally '\d' represents any digit.

## Author

by Gordon E. the video finding G.O.A.T. 
Github: https://github.com/G-code117

