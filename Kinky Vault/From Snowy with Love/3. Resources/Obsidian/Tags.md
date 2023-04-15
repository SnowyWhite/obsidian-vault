## Add a tag to a note
To create a tag, enter a hashtag symbol (#) in the editor, followed by a keyword. For example, `#meeting`.
You can also add the tag to the [metadata](https://help.obsidian.md/Editing+and+formatting/Metadata):

```yaml
---
tag: meeting
---
```

Or, add several tags:

```yaml
---
tags:
  - recipe
  - cooking
---
```

You can also add multiple tags on a single line by separating them using commas:

```yaml
---
tags: recipe, cooking
---
```

## Find notes using tags

To find notes using the [Search](https://help.obsidian.md/Plugins/Search) plugin, use the `tag` [search operator](https://help.obsidian.md/Plugins/Search#Search operators) in your search term, for example `tag:#meeting`.

You can also search for tags by clicking on them in your notes.

To find notes using the [Tags](https://help.obsidian.md/Plugins/Tags) plugin, select **Tags: Show tags** in the [Command palette](https://help.obsidian.md/Plugins/Command+palette), and then select the tag you want to search for.

## Nested tags

Nested tags define tag hierarchies that make it easier to find and filter related tags.
Create nested tags by using forward slashes (`/`) in the tag name, for example `#inbox/to-read` and `#inbox/processing`.
Both the [Search](https://help.obsidian.md/Plugins/Search) and [Tags](https://help.obsidian.md/Plugins/Tags) plugins support nested tags.

## Tag format

You can use any of the following characters in your tags:

-   Alphabetical letters
-   Numbers
-   Underscore (`_`)
-   Hyphen (`-`)
-   Forward slash (`/`) for [Nested tags](https://help.obsidian.md/Editing+and+formatting/Tags#Nested tags)

Tags must contain at least one non-numerical character. For example, #1984 isn't a valid tag, but [#y1984](https://publish.obsidian.md//#y1984) is.

Tags can't contain blank spaces. To separate two or more words, you can instead use the following formats:

-   [#camelCase](https://publish.obsidian.md//#camelCase)
-   [#PascalCase](https://publish.obsidian.md//#PascalCase)
-   [#snake\_case](https://publish.obsidian.md//#snake_case)
-   [#kebab-case](https://publish.obsidian.md//#kebab-case)