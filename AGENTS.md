Project overview
Atom is a hackable, cross‑platform text editor built on Electron. It uses web technologies (Node.js, JavaScript, CoffeeScript and Less) to provide a highly customisable editor. The upstream repository was archived in March 2023, but this fork aims to revive Atom by updating dependencies, fixing security issues and modernising the codebase.
Setup commands
To build or test Atom locally you need Git, Node.js ≥ 10.12, npm ≥ 6.12 and a recent Python (2.6/2.7/3.5+). Clone your fork and run the bootstrap script to install all dependencies:

git clone git@github.com:<your‑username>/atom.git
cd atom
script/bootstrap    # use script\bootstrap on Windows
If you cloned into a non‑default location, set the ATOM_DEV_RESOURCE_PATH environment variable to point to your local repository.
Start the editor in development mode to run from your source tree:

atom --dev path-to-open
Running in dev mode means you don’t have to rebuild every time you change code—just restart the app. When developing packages, install them in ~/.atom/dev/packages (or %USERPROFILE%\.atom\dev\packages on Windows); packages there override those installed globally.
Testing and building
Atom’s core uses Jasmine for unit tests. Before committing changes, ensure that tests pass by setting ATOM_DEV_RESOURCE_PATH and running:

cd path-to-your-local-atom-repo
atom --test spec
This runs the entire test suite locally. If you’re working on a package, include thoughtful specs under the ./spec directory; treat describe as a noun and it as a statement about state or how an operation changes state
To build a production bundle, execute script/build (or script\build on Windows). Use --install to install the app, or options such as --create-debian-package, --create-rpm-package or --create-windows-installer to build platform‑specific installers
Code style guidelines
Follow the style guides defined in CONTRIBUTING.md. Key points include:
Commit messages – Write in the present tense and imperative mood, keep the subject line under 72 characters, reference issues/PRs and include [ci skip] when only updating docs. Prefix commit messages with an appropriate emoji (e.g. :bug: for bug fixes)
JavaScript – The codebase is formatted with Prettier. Prefer the object spread operator ({…obj}) to Object.assign(), inline exports and order imports as built‑in modules, then Atom/Electron modules, then local Modules. Organise class members by static methods first, then instance methods and avoid platform‑specific code
CoffeeScript – Omit spaces around default parameter assignments (count=1), use spaces around operators, avoid spaces inside hash literals ({a: 1, b: 2}) and add a blank line between methods. Capitalise acronyms except for the first word (e.g. getURI instead of getUri) and prefer this over @. Use slice() when copying arrays.
Tests – Place specs in the ./spec directory and write clear Jasmine descriptions
Documentation – Write API documentation with AtomDoc and Markdown; refer to classes and methods using the {ClassName}, {ClassName::method} and {ClassName.method} notation
Pull requests and workflow
Always run script/bootstrap, atom --test spec and script/build before pushing. Address failing tests or lints locally.
Follow the commit and style guidelines above
Keep changes cross‑platform. Avoid hard‑coding OS‑specific paths or behaviours
When updating dependencies, use maintained libraries and run npm audit to check for vulnerabilities.
Consider adding or updating tests whenever you change behaviour.
Development tips
Reloading – Stylesheets reload automatically in dev mode, but JavaScript and CoffeeScript require reloading the window via window:reload
Environment variables – Use ATOM_DEV_RESOURCE_PATH to point Atom at your local source tree. Without it Atom may run the globally installed version
Windows quirk – If script commands (script\bootstrap or script\build) fail without errors, ensure the repository path has no spaces and try moving the clone to a shorter path (e.g. C:\atom)
Security considerations
Atom bundles many dependencies. When reviving the project, keep them up to date and resolve npm audit warnings promptly. Validate untrusted input and avoid executing arbitrary code in the main process. Carefully vet native modules to minimise attack surface.
Nested AGENTS.md files
For large monorepos, place additional AGENTS.md files in subdirectories (such as core packages) to provide package‑specific instructions. Agents will search for the nearest AGENTS.md and use that for context.
Living document
This file is meant to evolve. Update it whenever build commands, style rules, test setups or other project conventions change. A well‑maintained AGENTS.md helps AI coding agents understand your project and work effectively
