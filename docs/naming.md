# Naming

> Is it a bird? Is it a plane? No! It's a... var_1?!

Phil Karlton famously said:

> There are only two hard things in Computer Science: cache invalidation and naming things

Naming can be a contentious topic as it is heavily opinionated and open to preference and interpretation. Although choosing good names takes time, it saves more than it takes.

- Be explicit, not implicit
  - Descriptive
  - Unambiguous
- Be consistent - and aim to follow convention
- Use pronounceable words - programming requires collaboration and discussion
- Use searchable words - help others find what they are looking for
- Avoid abbreviations
- Avoid types
- Include units e.g. `delaySeconds` unless the type tells you
  - e.g. use `delay` for a datetime object, instead of `delayDatetime`
- Avoid use of `Base` or `Abstract` in naming i.e. use `Student` instead of `AbstractStudent`
- Sometimes structure needs to be changed. Refactor if you have 'utils' or 'helpers', consider whether its right to have them in same module
- Prefer "from" over "to", like `pdf_from_html` instead of `html_to_pdf`. This keeps related names physically closer, as in `pdf = pdf_from_html("file.html")`

If you are still having trouble naming something, it probably means something needs to be restructured in the code.

## References

- _Clean Code_, Robert C. Martin
- [Small Naming Tip: Use "from" Instead of "to" in Function and Variable Names](https://lesleylai.info/en/from-vs-to/), Lesley Lai
