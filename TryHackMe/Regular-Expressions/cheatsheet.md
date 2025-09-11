# Regex Cheatsheet

## Concepts And Patterns

| Concept / Feature           | Pattern / Example           | Notes / Usage                           |
|-----------------------------|----------------------------|----------------------------------------|
| **Charsets**                | `[abc]`                    | Matches any character a, b, or c       |
|                             | `[a-c]zz`                  | Range for first char; matches azz, bzz, czz |
|                             | `[a-zA-Z]`                 | Any letter, lower or uppercase         |
|                             | `[^k]ing`                  | Excludes k; matches ring, sing, $ing  |
| **Wildcards & Optional**    | `.`                        | Matches any single char except line break |
|                             | `?`                        | Makes preceding char optional          |
|                             | `\.`                       | Literal dot                             |
| **Metacharacters**          | `\d`                       | Any digit (0-9)                        |
|                             | `\D`                       | Non-digit                               |
|                             | `\w`                       | Alphanumeric + underscore              |
|                             | `\W`                       | Non-alphanumeric                        |
|                             | `\s`                       | Whitespace (space, tab, newline)       |
|                             | `\S`                       | Non-whitespace                          |
| **Repetitions / Quantifiers**| `*`                        | 0 or more                               |
|                             | `+`                        | 1 or more                               |
|                             | `{n}`                      | Exactly n times                          |
|                             | `{m,n}`                    | Between m and n times                   |
|                             | `{m,}`                     | m or more times                          |
| **Anchors**                 | `^pattern`                 | Line starts with pattern                |
|                             | `pattern$`                 | Line ends with pattern                  |
| **Groups & Either/Or**      | `(pattern)`                | Groups characters or pattern            |
|                             | `pattern1|pattern2`        | Either/or pattern                        |
|                             | `(no){5}`                  | Repeats group 5 times                    |


# Regex Problems & Solutions Cheatsheet

### Charsets

| Problem / Task                                    | Regex Solution    | Notes / Explanation                               |
|--------------------------------------------------|-----------------|--------------------------------------------------|
| Match characters: c, o, g                        | [cog]           | Matches any single character in the set          |
| Match words: cat, fat, hat                        | [cfh]at         | Matches any first character from the set         |
| Match words: Cat, cat, Hat, hat                   | [CcHh]at        | Case-sensitive matching                           |
| Match filenames: File1-File5, File7, file9       | [Ff]ile[1-9]    | Matches F/f + "ile" + digits 1-9                 |
| Match filenames of above, except File7           | [Ff]ile[^7]     | Excludes 7                                        |

### Wildcards & Optional Characters

| Problem / Task                                    | Regex Solution    | Notes / Explanation                               |
|--------------------------------------------------|-----------------|--------------------------------------------------|
| Match words: Cat, fat, hat, rat                  | .at             | `.` matches any single character                 |
| Match words: Cat, cats                             | [Cc]ats?        | `?` makes preceding character optional           |
| Match domain: cat.xyz                              | cat\.xyz        | `\.` matches literal dot                          |
| Match domains: cat.xyz, cats.xyz, hats.xyz        | [ch]ats?\.xyz   | Optional character + literal dot                  |
| Match 4-letter strings not ending n-z             | ...[^n-z]       | `[^n-z]` excludes range at last position         |
| Match bat, bats, hat, hats, not rat(s)           | [^r]ats?        | Excludes "r" at start                             |

### Metacharacters & Repetitions

| Problem / Task                                    | Regex Solution     | Notes / Explanation                              |
|--------------------------------------------------|-----------------|-------------------------------------------------|
| Match: catssss                                    | cats{4}          | `{4}` repeats preceding character exactly 4x    |
| Match: Cat, cats, catsss                          | [Cc]ats*         | `*` repeats 0 or more times                     |
| Match sentences: regex go br, regex go brrrrrr   | regex go br+     | `+` repeats 1 or more times                     |
| Match filenames: ab0001, bb0000, abc1000 ...     | [abc]{1,3}[01]{4}| `{1,3}` repeats 1-3 chars, `[01]{4}` 4 digits  |
| Match filenames: File01, File2, file12...        | [Ff]ile\d{1,2}  | `\d{1,2}` 1 or 2 digits                          |
| Match folder names: kali tools, kali     tools    | kali\s+tools     | `\s+` matches 1+ whitespace                      |
| Match filenames: notes~, stuff@, gtfob# ...      | \w{5}\W          | 5 alphanum chars + 1 non-alphanum char          |
| Match string in quotes with spaces/symbols       | \S*\s*\S*        | `\S*` non-whitespace, `\s*` whitespace          |
| Match 9-character strings not ending with !      | \S{8}[^!]        | 8 non-whitespace + not `!`                       |
| Match: .bash_rc, .unnecessarily_long_filename... | \.?\w+           | Optional dot + 1+ word characters               |

### Anchors, Groups & Either/Or

| Problem / Task                                    | Regex Solution     | Notes / Explanation                              |
|--------------------------------------------------|-----------------|-------------------------------------------------|
| Match strings starting with "Password:" + 10 chars not 0 | Password:[^0]{10} | `[^0]{10}` 10 chars excluding 0                 |
| Match "username: " at start of line             | ^username:\s      | `^` anchors start, `\s` matches space           |
| Match lines not starting with a digit           | ^\D               | `\D` non-digit at start                          |
| Match "EOF" at end of line                       | EOF\$             | `$` anchors end, escape `$`                      |
| Match sentences: I use nano, I use vim         | I use (nano|vim)  | Either/or with group                              |
| Match lines: $, digit, $, 1+ non-whitespace chars | \$\d\$\S+         | Escape `$`, `\d` digit, `\S+` one+ non-space    |
| Match all IPv4 addresses                        | (\d{1,3}\.){3}\d{1,3} | Groups + repetition for octets                   |
| Match emails with username & domain in groups  | (\w+)@(\w+)\.com | Groups capture username & domain                  |
