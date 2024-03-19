# Console

## The Long and Short of Option Names

Reserve shorthand command-line option names for the console - where they are efficient. Always use long names in scripts. Shorthand condenses code, but at the detriment of readability and explicitness.

While shorthand names may be intuitive when written, or to a tool expert...

```console
radon cc -asj .
```

...long names provide a more meaningful, human-readable representation at all times for all readers.

```console
radon cc --average --show-complexity --json .
```

## Taking Shortcuts

When we consider opportunities to optimise our workflow, we typically focus on the larger and more evident chunks of time, such as reducing the number of meetings or blocking focus time for deep work. While improving these areas is very important, it is easy to overlook micro-optimisations. We can become accustomed to suboptimal behaviours through habit or be unaware of improved methodologies. These behaviours can add up to significant productivity loss and continuously hamper our focus.

So what can we do about it?

### Automate

> Automate the boring stuff

Seek out opportunities to transform tedious manual tasks into powerful automations.

Spend some time to filter out noise from emails, optimise your tooling, or even build an ecosystem of tools to support your development; the possibilities are limitless.

For example, you could automate formatting that you manually apply to maintain a clean code base, just like [pyprojectsort](https://github.com/kieran-ryan/pyprojectsort).

### Alias

Aim to do more with less. Save yourself precious keystrokes and replace long, frequent commands with an alias.

Cumbersome commands that require tool-specific knowledge and high cognitive load...

```console
pytest --cov-config .coveragerc --verbose --cov-report term --cov-report xml --cov=pyprojectsort tests
```

...can be greatly simplified with tools such as `make`; improving development workflows and standardising commands across projects.

```console
make coverage
```

Having a handy set of utility aliases that simplify frequent commands can be a great way to move with speed on the command line.

```console title="Example: Change directory alias"
alias .. = 'cd ..'
alias ... = 'cd ../..'
alias .... = 'cd ../../../'
```

### Find a Buddy

Continuously confide in the feedback of others. Find people that support and identify areas where you can approve - this is one of the most valuable feedback loops you can have.

A developer can get wrapped up in their own bubble of tools and ways of working. Objective, external feedback can provide a valuable, unbiased and fresh perspective that can help break from that cycle.

### Get to Know Your Tools

The tools we use are the bedrock of our development experience. Getting to know them well can keep us moving and make for a more effortless workflow.

Despite this, many struggle with tools they use every day, such as git.

How can you change this?

Studies have shown using a keyboard is significantly faster compared to using a mouse. A light approach for learning keyboard shortcuts can be to set aside some time every now and then to understand them intimately. Shortcut helpers - such as [Key Promoter X](https://plugins.jetbrains.com/plugin/9792-key-promoter-x) in PyCharm - can notify you every time you clicked through a process that has an alternative keyboard shortcut. Reading the tool documentation or following a tutorial are always good options. A more brutalist approach can be to restrict yourself completely, such as to disconnect your mouse for a week; this will force you to restrict yourself and to learn shortcuts much faster.

### Summary

The next time you find yourself leaving the keyboard and reaching for your mouse, ask yourself "Is there a way I could perform this task from the keyboard?", find out and give it a try.

## References

- [Don't use short options in scripts](https://www.youtube.com/watch?v=OKqWy2dM2Jo) - Anthony Sottile ([@asottile](https://github.com/asottile))
- [Physically disable your mouse for a week](https://twitter.com/mitchellh/status/1758547659282174092)
