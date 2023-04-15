# Overview

Here are things good to know when working with Visual Studio.


## Regex Patterns for Find and Replace

### Remove around argument
To remove everything before the first argument ($1), you can use a positive lookbehind assertion in your regular expression pattern. Here is an example pattern:

```regex
(?<=Foo\.Bar\()([^)]*)
```

Find: ``(?<=Foo\.bar\()([^)]*)``
Replace: `$1`

In this pattern, the ``(?<=Foo\.bar\()`` is the positive lookbehind assertion, which checks that the match is preceded by the string `Foo.bar(` without including it in the match. 
The `([^)]*) ` matches and captures any characters that are not a closing parenthesis, which is the argument passed to `Foo.bar()`.
The `$1` in the replacement text inserts the captured argument.

So, if you apply this pattern to the string `string x = Foo.bar(i) + j;`, the result would be `string x = i + j;`.

### Replace before argument

Here is an example regex pattern that you can use in Visual Studio's Find and Replace dialog:

```regex
Foo\.bar\([^)]*\)
```

Find: `Foo\.bar\([^)]*\)`
Replace: `MyNewMethod($&)`

This regex pattern will find all instances of `Foo.bar()` and capture the entire method call, including the parentheses and any arguments within them. 
The `$&` in the replacement text will insert the entire captured match into the replacement text.

You can replace `MyNewMethod` with the name of the new method you want to use instead of `Foo.bar`.

For example, if you want to replace "Foo.bar" with "MyNewMethod" and remove everything after "i", you can use the following regex pattern:

Find: `Foo\.bar\((.*?)\).*$`
Replace: `MyNewMethod($1)`

This regex pattern will capture the argument passed to `Foo.bar()` and use it in the replacement text as the argument for `MyNewMethod()`. 
The `.*$` at the end of the pattern matches any characters after the argument, which will be removed in the replacement.

### Replace from line begin to symbol

This pattern matches the beginning of the line (`^`), followed by the literal string "foo bar", one or more whitespace characters (`\s+`), 
one or more non-equal sign characters (`[^=]+`), and finally an equal sign (`=`):

```regex
^foo\s+bar\s+[^=]+=
```

Note that if there are any other characters on the line after the equal sign, they will also be selected by this pattern. 
If you want to select only the text up to the first equal sign, you can modify the pattern to include a non-greedy quantifier (`*?`) after the `[^=]+` group, like this:

```regex
^foo\s+bar\s+[^=]+*?=
```