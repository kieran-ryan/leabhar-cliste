# Naming

> Is it a bird? Is it a plane? No! It's a... var_1?!

As Phil Karlton famously quipped, the two hardest aspects of Computer Science are cache invalidation and naming things.

Naming can indeed be a subject of much debate due to its subjective nature and room for interpretation. While it takes time to choose meaningful names, the clarity it brings is a worthy investment.

Here are some guidelines to help you achieve meaningful names:

- Prioritise clarity and avoid ambiguity. Names should be descriptive and explicit.
- Maintain consistency. Strive to follow established conventions.
- Use pronounceable and searchable words. Programming is a collaborative effort, and others may need to discuss or locate your code.
- Avoid abbreviations and types.
- Include units in names, such as `delaySeconds`, unless the type already implies it - such as `delay` for a datetime object, rather than `delayDatetime`.
- Refrain from using `Base` or `Abstract` - such as `Student` instead of `AbstractStudent`.
- Favour "from" over "to", such as `pdf_from_html` instead of `html_to_pdf`. This keeps related names closer, as in `pdf = pdf_from_html("file.html")`.
- If you find yourself creating `utils` or `helpers`, reconsider their placement. Difficulty in naming might signal a need for code restructuring.

## References

- _Clean Code_, Robert C. Martin
- [Small Naming Tip: Use "from" Instead of "to" in Function and Variable Names](https://lesleylai.info/en/from-vs-to/), Lesley Lai
