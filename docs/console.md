# Console

## Long Option Names

Reserve shorthand option names for the console - where it is most efficient. Always use long names in scripts. Shorthand condenses code, but at the detriment of readability and explicitness.

While shorthand names may be intuitive when written, or to a tool expert...

```console
radon cc -asj .
```

...longhand provides a more meaningful, human-readable representation at all times for all readers.

```console
radon cc --average --show-complexity --json .
```

## Aliases

Use aliases to optimise your workflow.

```console
alias .. = 'cd ..'
alias ... = 'cd ../..'
alias .... = 'cd ../../../'
```
