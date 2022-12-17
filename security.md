# Dependency Confusion

"dependency confusion" is a supply chain exploit where a hacker provides their malicious package with the same name as a genuine package and uploads it to a public repository in the hope that it's accidentally downloaded. If successful, the hacker will have access to [arbitrary code execution](https://www.okta.com/identity-101/arbitrary-code-execution/), potentially allowing them full access to sensitive data or enabling them to damage production services.

To prevent this exploit, ensure all dependencies are:

- "pinned" to a specific version
- "pinned" to a hash of a version's contents
- Pulled from a single secure server
  - Mirrored to the server if they are public

## Remediation Example

For Python dependencies, using a private PyPi server in combination with the public PyPi poses a number of security risks.

Do not use "pip --extra-index-url". It does not honour any ordering of whether to prioritise packages from the private or public PyPi server for name collisions.

Do:

- Use a single server endpoint that manages priorities on the backend
  - Artifactory supports virtual repositories that allow you to use a single endpoint that then "virtually" dispatches to an appropriate backend repository, including features like prioritisation. That means you can configure Artifactory to always prioritise private repositories.
- Mirror public packages to your private PyPi
- Tie dependency installation to a hash of the contents rather than just the name and version of the package
  - Even if the name and package are the same, if any contents are different than expected, installation will fail. This can be done with tools like `pip-tools` and `poetry`.
- Consider "squatting" a similarily named package on PyPi (creating an empty package to prevent others pushing malicious packages to that namespace), however this is not endorsed by the PyPi organisation and empty packages can be removed.
  - It also exposes your package names and naming conventions - which provides more information to attackers e.g. they could try the same naming conventions on a different unprotected package repository, such as `npm`.

# Email

When signing up for a service, include the site name in your email address e.g. `email+site@gmail.com`. If you receive any spam over that address, you will know that they sold your data, and you can more easily filter out and identify spam emails against that address.
