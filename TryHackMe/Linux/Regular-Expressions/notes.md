# Regex Notes

**These notes summarize my learning from TryHackMe's Regular Expressions Room.**

## Introduction
- Regular expressions are text patterns used to search, match, and manipulate text efficiently. Learning Regex is valuable for problem-solving, CTF challenges, and coding tasks, saving time and improving accuracy.


## Charsets

**Concepts Learned:**  
- How to match specific characters in a text or file.  
- How to define character ranges and combine them.  
- How to exclude certain characters or ranges.  

**Patterns / Usage:**  
- `[abc]` → matches a, b, or c.  
- `[abc]zz` → matches azz, bzz, czz.  
- `[a-c]zz` → defines a range; same as above.  
- `[a-cx-z]zz` → combines ranges; matches azz, bzz, czz, xzz, yzz, zzz.  
- `[a-zA-Z]` → matches any letter, lowercase or uppercase.  
- `file[1-3]` → matches file1, file2, file3.  
- `[^k]ing` → excludes k; matches ring, sing, $ing.  
- `[^a-c]at` → excludes a-c; matches fat, hat.  

**Notes:**  
- Charsets match **individual characters**, not whole strings.  
- Keep characters in the same order as the pattern requirements.  
- Efficient regex is key:  
  - Be specific enough for the task.  
  - Avoid unnecessary complexity; simple and concise patterns are preferred.  
- Multiple correct solutions may exist; the goal is the most efficient pattern for the given problem.



## Wildcards & Optional Characters

**Concepts Learned:**  
- How to match any single character using a wildcard.  
- How to make a character optional in a pattern.  
- How to escape special characters to match them literally.  

**Patterns / Usage:**  
- `.` → matches any single character except line breaks.  
  - Example: `a.c` matches `aac`, `abc`, `a0c`, `a!c`, etc.  
- `?` → makes the preceding character optional.  
  - Example: `abc?` matches `ab` and `abc`.  
- `\.` → escapes the dot to match it literally.  
  - Example: `a\.c` matches only `a.c`, not `abc` or `a0c`.  

**Notes:**  
- Wildcards provide flexibility but can match unintended characters; use carefully.  
- Escaping is necessary for special regex symbols when you want literal matches.



## Metacharacters & Repetitions

**Concepts Learned:**  
- How to use metacharacters to match common character types efficiently.  
- How to repeat patterns using quantifiers to match multiple occurrences.  
- Difference between exact, range, and unlimited repetitions.  

**Patterns / Usage:**  
- Metacharacters:  
  - `\d` → matches any digit (0-9)  
  - `\D` → matches any non-digit  
  - `\w` → matches alphanumeric character including underscore  
  - `\W` → matches non-alphanumeric characters  
  - `\s` → matches whitespace (spaces, tabs, line breaks)  
  - `\S` → matches non-whitespace characters  

- Repetitions / Quantifiers:  
  - `{n}` → exactly n times (e.g., `z{2}` matches `zz`)  
  - `{m,n}` → between m and n times (e.g., `a{1,5}`)  
  - `{m,}` → m or more times (e.g., `b{2,}` matches `bb`, `bbb`, ...)  
  - `*` → 0 or more times  
  - `+` → 1 or more times  

**Notes:**  
- Underscores `_` are included in `\w` but not in `\W`.  
- Quantifiers are applied to the preceding character, metacharacter, or charset.  
- Efficient use of metacharacters + repetitions can greatly simplify regex patterns.




## Anchors, Groups & Either/Or Patterns

**Concepts Learned:**  
- How to specify patterns at the start or end of a line using anchors.  
- How to group patterns together for clarity or repetition.  
- How to define alternatives using "either/or" logic in regex.  

**Patterns / Usage:**  
- Anchors:  
  - `^pattern` → matches lines that start with `pattern`  
  - `pattern$` → matches lines that end with `pattern`  

- Groups:  
  - `(pattern)` → groups a sequence of characters or patterns together  
  - Useful for applying repetitions or specifying alternatives  

- Either/Or:  
  - `pattern1|pattern2` → matches either `pattern1` or `pattern2`  
  - Example: `during the (day|night)` matches both `during the day` and `during the night`  

- Combined Repetition with Groups:  
  - `(no){5}` → matches `nonononono`  

**Notes:**  
- The `^` symbol is context-sensitive: inside `[]` it excludes characters, outside it anchors to the start of a line.  
- Groups make complex patterns easier to read and manage.  
- Efficient use of either/or patterns can reduce overly long regex expressions.



## Key Takeaways

- Regular expressions are a powerful tool for searching and pattern matching in text.  
- Start simple: think specific, but avoid overcomplicating patterns.  
- Reuse existing patterns (like for emails) when applicable, instead of reinventing the wheel.  
- Mastering regex improves efficiency in text processing, CTF challenges, and development tasks.  
- Continuous practice and online resources help solidify understanding and skill.  
- Enhances problem-solving and critical thinking skills while analyzing text patterns.


