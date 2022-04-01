# Deconstructing URL's

Whenever we browse the internet, the first thing we will do, outside of opening the browser, is input our web domian into the search field in order to be taken to the website we want to visit... ie `gooogle.com`
Our broswer input is usually unique and specific to the website we want to visit. ie, `google.com` will take us to the google homepage. 
We can easily identify a number of websites by the domains as we know them:

`google.com`
`apple.com`
`yahoo.com`

Whilst each of these URL's are unique to the sites we'll visit, they do have a few things in common. 

### a) they are represented by a string, ie 'google'
### b) they are seperated by a fullstop ie '.'
### c) they all end in '.com'

If we breakdown these identifiers into a generic format, we're left with the following expression:

`/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

The above expression is the foundational blueprint of every website we visit. This line gives us the 'regular expression' OR regex of a URL without specifying the unique path we'll use to access our websites (ie, `google.com`).

## Summary

Today, we'll look at th regular expressions of URL's more specifically, breaking down their components so we can understand why when we enter them into our browsers, we are routed to websites we've selected. 

Let's start by reviewing the regex itself by it's components.

## Table of Contents

- [Regular Expressions](#regular-expressions)
  - [Summary](#summary)
  - [Table of Contents](#table-of-contents)
  - [Regex Components](#regex-components)
    - [Anchors](#anchors)
    - [Quantifiers](#quantifiers)
    - [Grouping Constructs](#grouping-constructs)
    - [Bracket Expressions](#bracket-expressions)
    - [Character Classes](#character-classes)
    - [The OR Operator](#the-or-operator)
    - [Flags](#flags)
    - [Character Escapes](#character-escapes)
  - [Author](#author)

## Regex Components

A regex is considered a literal, so out pattern will always be bookended by slashes (/). If we look at the “URL” regex, you'll see how this applies:

`/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

### Anchors

URL's use anchors. 
Anchors are characters that represent strings of our URL has begun and are symbolised by `^` and `$` icons in the regex expression. 

We use `^` anchor to inform our expression that a string will then proceed beyond the character:

ie, `^hello`

We use `$` anchor to signify that a string has ended and that characters have proceeded it. It has the opposite effect to the `^` character.

In our URL expression, we use `^` after our initial / brackets to indicate a string will follow, and a `$` before our final / to indicate a string will proceed the last component of the URL.



### Quantifiers

Quantifiers are used to fix the minimum and maximum lenght of the string that your regex matches or a indiviudaul component of the string. 

They set limits to the numbers of characters that your regex is looking for.

You'll notice the `{2,6}` grouping of numbers at the end of our expression. This indicated the character length of that URL's component. 

Sometimes we finish website domains with `.com`, `.net` or `.gov` - each of these strings, proceeding the '.' are limited to exist between 2 and 6 characters, as per the limit set by our regex.

### Grouping Constructs

Grouping constucts assist us in breaking up complex parts of the regex. This is particularly immportant when it comes to URL domains, given that we have multiple items that need seperation in order to have their unique parameters set. 

In order to group components of our URL, we use parentheses `()` that act as seperators so we can apply our regex to these sections. 

For example, at the opening of our URL regex, we use `(https?:\/\/)` - this is fixed within the group construct as every webdomain begins with http or https. We dont always choose to use this when we access our websites, but this is written as a group as it is needed for every site we visit. 

As we transcend the regex, other grouped constructs exist to allow us to apply specific parameters to specific componenets drawn from what we apply within our regex. 

When nesting within `()`, we search for an exact match unless told to do otherwise. 


### Bracket Expressions

We've talked about parentheses, however you'll notice in the regex for our URL, we also use square brackets as well `[]`.

Whilst parentheses assist us in grouping componenets of our URL, square brackets are used when we want to outline the characters we want to use. 

Bracket expressions are less constricted than grouped constructs because the only need to find partial matches to a string rather than the the exact form as displayed in the regex. 

As per our URL expression, we have this componenet `([\da-z\.-]+)` proceeding the http group. As we have used the hyphen, `a-z` we can search for any letters between a and z in lowercase. 

As there is no quantifier rule, our entries can be as long as possible, however most web domains are kept fairly brief as it improves user experience (ie, `google.com`).

### Character Classes

In the bracket expression, you would have noticed the `d` sitting before the `a-z`.

This is known as a Character class which defines a specific set of characters that can also be used to in out input to complete a match. 

Here are some examples of character classes:

`\d` matches any arabic numberal digit. This class is equivalent to the bracket expression [0-9] meaning we dont need to request the full range of numbers in order to acheive the same outcome. 

`\w` matches any alphanumeric character from the latin alphabet. It is the same as writing `[A-Za-z0-9].

`\s` Matches a single whitespace character, including tabs and line breaks.

Each of these can be changed to capitalise our characters if we want to by capitalising the class itself, ie `\D`.

### The OR Operator

The OR operator, is written like `\` and converts our prevents our input, particularly within a grouping construct, from needed to match the input exactly. 

For example, if we had `(listen)` within a group, our input would need to match `listen` in the exact order. The Or operator helps us prevent this so our input can contain the same characters, but doesnt need to match exactly. 

We would write this in the following format - `(l|i|s|t|e|n)` - in this way, other strings, ie `slient` would also be accepted as the Or operator allows for acceptances in different orders.


### Character Escapes

We use the `\` backslash expression to prevent us from interpreting a character literally. 

In our URL regex, the domain name construct is written as `([\da-z\.-]+)` and we include the backslash before the character class to prevent the expression from reading the `d` character literally. 

This backslash indicates a characater class is in use, and we prevent overreading of our expressions by included these tags. 

## Author

This contents was written by Oscar Bryant, Coding Bootcamp Student, 2022.
https://github.com/oscarcbryant
