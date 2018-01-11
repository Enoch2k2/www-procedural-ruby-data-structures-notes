# Hash manipulation and Regex Notes (WWW Procedural Ruby IV Data Structures)

### Hashes

Hashes like array's are a collection of data. We create a hash, and inside that hash we give it data using key / value pairs.

Example of creating a hash:
```
hash = Hash.new

or

hash = {}
```

Example of giving a hash a key / value:
```
hash = {
    name: "Bob",
    age: 42,
    employed: true
}

or

hash = {}
hash[:name] = "Bob"
hash[:age] = 42
hash[:employed] = true

in this particular format of hash[:key], if they key doesn't yet exist in the hash, it will create the key and set it's value
```

we can also give it nested collection as values such as other hashes or arrays, for example:
```
hash = {
    name: "Bob",
    age: 42,
    children: [
        {
            name: "sally",
            age: 7
        },
        {
            name: "billy",
            age: 2
        }
    ]
}

```

With hashes and selecting nested collections, you can think about the values you are selecting and work off of those values, for example: 
```
bob = {
    name: "Bob",
    age: 42,
    wife: {
        name: "Mary",
        age: 40
    }
}

then we can access the name of bob's wife like this:

bob[:wife][:name] <= which would give us "Mary"

we are first selecting the hash (bob)
then the wife [:wife] which gives us the hash {name: "Mary", age: 40}
then we access the wife's name with bob[:wife][:name] <= "Mary"
```

creating nested collections inside of hashes conceptual examples:
```
bob = {
    name: "Bob",
    age: 42
}
```

with bob if we wanted to create the wife hash as in the previous example, we cannot automatically assume the hash datatype has yet been created, for example:
```
bob[:wife][:name] = "Mary"
```

This would end up breaking our code, we would first need to establish bob[:wife] as a hash before ruby recognizes it as a hash.
```
bob[:wife] = {}
bob[:wife][:name] = "Mary"
```

### Regex

Regex is a strong pattern like structure to validate data. It can seem intimidating at times. And look very strange in the way it's setup, for example: `/^\w+@\w+\.com$/` which would validate an email.

Ways to handle regex:

- I strongly recommend using [Rubular](http://rubular.com/) in order to practice your regex.

Regex CheatSheet:
```
^ - start of line
$ - end of line
[] - any single character
\w - any word character (ex: letter, number, underscore)
+ - 1 or more of a character (helpful if there is at least 1 character and also if you don't know how many characters there will be)

example: /^[aeiouAEIOU]\w+$/ checks the line if a word starts with a vowel.

? - optional character

example: /^h?g?e?o?l?o?l?d?o?b?y?e?$/ validates the the word is either hello / goodbye or any substring / characters inside the regex. h? means an h could be included, g? means a g could be included ect. (This is not how you would validate hello or goodbye thoroughly just an example of how the ? works.)

\d - any digit
\D - any non digit
\s - any whitespace character
\S - any non whitespace character
\W - any non word character
\b - any 'word' boundary (will check words, any characters that has a white space in front and after the characters)
{x} - where x is an integer, will be exactly x of a character.
```
##### Scan
The scan method when used on a string will return an array of substrings (strings taken from a string) that is matched by the regex. Example:
```
the regex is looking for a 4 letter word
"hello world, this is your leader speaking".scan(/\b\w{4}\b/)

returns ["this", "your"]
```

### Match
Match returns match data and is good if you are checking the string to make sure it matches the regex, example:
```
the regex is looking for a 5 letter word that starts with capitalization

"Hello".match(/\b[A-Z]\w{4}\b/)
returns #<MatchData "Hello">

"hello".match(/\b[A-Z]\w{4}\b/)

returns nil
```