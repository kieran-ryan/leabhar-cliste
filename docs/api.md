# API

When designing APIs, it's crucial to focus on discoverability, intuitiveness, flexibility, and simplicity.

## Discoverability

Discoverability is about making it easy for users to find and utilise the features of your API. There are five key elements of discoverability:

- **Affordances:** Possible actions that users can take with your API. Good affordances are intuitive and easy to understand.
- **Signifiers:** Indicators that point to the affordances. In an API, good signifiers could be well-named endpoints that clearly indicate their functionality.
- **Constraints:** Limitations on what can be done with your API. Constraints can guide users towards correct usage.
- **Mappings:** Relationships between actions and outcomes. Good mappings in an API make it clear what will happen when a certain request is made.
- **Feedback:** Response users get after they perform an action. Good feedback in an API is informative and helps users understand the result of their actions.

## Tenets of Good APIs

A well-designed API should be:

- **Intuitive:** It should use domain-specific language, making it easier for users familiar with the domain to understand. Clumsy naming often indicates clumsy abstractions. The API should also provide symmetry, meaning similar actions have similar interfaces.
- **Flexible:** It should provide sane defaults, but also allow users to customise behaviours through optional keyword arguments. It should minimise repetition, allowing users to achieve their goals with less code. In essence, a good API lets users be lazy.
- **Simple:** It should provide composable functions, allowing users to build more complex operations from simpler ones. It should leverage language idioms, making it feel like a natural extension of the programming language. Lastly, it should provide convenience, making common tasks easy to perform.

By following these principles, you can create APIs that are easy to learn, use, and remember.

## References

- [The Design of Everyday APIs](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwj2297gmPGAAxVqWkEAHYvGCigQz40FegQIHBAp&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3D0qYDmm1O7hc&usg=AOvVaw134I82h7uW0iYSeKYdssNv&opi=89978449), Lynn Root
