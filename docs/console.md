# Console

## The Long and Short of Option Names

Reserve shorthand command-line option names for the console - where they are efficient. Always use long names in scripts. Shorthand condenses code, but at the detriment of readability and explicitness.

While shorthand names may be intuitive when written, or to a tool expert...

```console
radon cc -asj .
```

...long names provide a meaningful representation always for all readers.

```console
radon cc --average --show-complexity --json .
```

## Default To Defaults

Software development is famous for intense debates that distract from problem solving without achieving meaningful outcomes: [single or double quotes](https://github.com/psf/black/issues/118), tabs versus spaces, best language, best framework, and so on.

While these discussions may endure, we can reduce disagreements within teams and encourage progress.

One strategy is following tool default settings. This ensures compliance with conventions while avoiding unnecessary complexity through customisation. We can enhance this approach by choosing highly opinionated tools, saving time and energy for more important matters.

![image](https://external-preview.redd.it/EcwKGjcxeR77frd8nFeG2ggEpCSLtGbudsABDPGBTe8.png?auto=webp&s=738e71260d3ec2e1f8ec863ad3f1de9b6aff51ad)

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

- [Black - The uncompromising code formatter](https://black.readthedocs.io/en/stable/) - Opinionated Python formatter which eliminates discussion around code formatting.
- [CLI tool to correct mistakes in previous command](https://github.com/nvbn/thefuck?tab=readme-ov-file#experimental-instant-mode)
- [Don't use short options in scripts](https://www.youtube.com/watch?v=OKqWy2dM2Jo) - Anthony Sottile ([@asottile](https://github.com/asottile))
- [Oh-My-Zsh git aliases](https://kapeli.com/cheat_sheets/Oh-My-Zsh_Git.docset/Contents/Resources/Documents/index)
- [Physically disable your mouse for a week](https://twitter.com/mitchellh/status/1758547659282174092)
- [The Power of Defaults](https://blog.codinghorror.com/the-power-of-defaults/)
- [Zsh plugin to help remember your aliases](https://github.com/djui/alias-tips)
