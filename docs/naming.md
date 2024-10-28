# Naming

> Is it a bird? Is it a plane? No! It's a... var_1?!

As famously quipped by Phil Karlton, '_There are only two hard things in Computer Science: cache invalidation and naming things_'.

Naming can indeed be a subject of much debate due to its subjective nature and room for interpretation. However, while it takes time to choose meaningful names, the clarity it brings makes it a worthwhile endeavour.

Here are some guidelines to help you achieve meaningful names:

- Prioritise clarity and avoid ambiguity. Names should be descriptive and explicit.
- Maintain consistency. Strive to follow established conventions.
- Use pronounceable and searchable words. Programming is a collaborative effort, and others may need to discuss or locate your code.
- Use 'explanatory variables', separating complex statements into smaller, named pieces of code - improving comprehension.
- Avoid redundant context
  - Refrain from using `Base` or `Abstract` i.e. use `Student` instead of `AbstractStudent`.
  - Include units in names, such as `delaySeconds`, unless the type already implies it - such as `delay` for a datetime object, rather than `delayDatetime`.
- A long, descriptive name is better than a name that is short and ambigious.
  - Long names can impact horizontal scrolling and make it harder to analyse associate code at a glance. This can however hint that code design can be improved.
  - Avoid abbreviations and types.
  - Follow the [Single Truth Rule](https://ruthlesslyhelpful.net/2012/02/25/rules-for-commenting-code), using expressive naming _"The compiler should use the same variable to represent the same single true meaning that the human reader understand"_ where a comment may have been used as mitigation for poor naming. If a comment says what the code **could** say, change the code.
- If you find yourself creating `utils` or `helpers`, reconsider their placement. Difficulty in naming might signal a need for code restructuring.

### Favour 'from' over 'to'

When converting or translating values, using `_to_` within function names is common.

However, this tends to separate naming from usage, fragmenting the flow for the reader.

```python
def html_to_pdf(html):
    ...

pdf = html_to_pdf("file.html")
```

Alternatively, using `_from_` keeps related names closer: with the output described closest to assignment, and with the input described closest to the argument.

```python
def pdf_from_html(html):
    ...

pdf = pdf_from_html("file.html")
```

This aligns closely with the functional programming idiom of naming the function after the result it produces.

## References

- [Do's and Don'ts of Commenting](https://blog.openreplay.com/dos-and-donts-of-commenting-code/?utm_source=tldrwebdev)
- _Meaningful Names, Chapter 2 - Clean Code_, Tim Ottinger
- [Meaningful Names Revisited](https://www.industriallogic.com/blog/meaningful-names-revisited/), Tim Ottinger
- [Rules for Commenting Code](https://ruthlesslyhelpful.net/2012/02/25/rules-for-commenting-code/), Ruthlessly Helpful, Stephen Ritchie
- [Self-documenting Code](https://lackofimagination.org/2024/10/self-documenting-code/?utm_source=tldrwebdev)
- [Small Naming Tip: Use "from" Instead of "to" in Function and Variable Names](https://lesleylai.info/en/from-vs-to/), Lesley Lai
