# Complexity

> Complexity is anything related to the structure of a software system that makes it hard to understand or modify the system

Complexity manifests itself in three general ways:

- **change amplification** - simple change requires code modification in many places
- **cognitive load** - how much a developer needs to know to complete a task
- **unknown unknowns** - code changes to complete a task are not obvious

Complexity is caused by:

- **dependencies** - occur when a given piece of code can not be modified in isolation without considering/modifiying another piece of code
  - leads to **change amplification** and a high **cognitive load**
- **obscurity** - occur when important information is not obvious
  - creates **unknown unknowns** and contributes to **cognitive load**

Modern software systems are intrinsic with complexity, and the skill requirements that constitute _full stack_ development are evergrowing. However, movements to revert to fundamentals - such as [Radical Simplicity](https://www.radicalsimpli.city/) - appear to be gaining traction back to a leaner stack.

## References

- _A Philosophy of Software Design_, John Ousterhout
- _[Radical Simplicity in Technology](https://www.radicalsimpli.city/)_, Stephen Schmidt
