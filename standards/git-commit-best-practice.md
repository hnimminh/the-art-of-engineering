# Git Commit - Best Practice

## Basic Rules
##### Commit Related Changes
* A commit should be a wrapper for related changes. For example, fixing two different bugs should produce two separate commits.
* Small commits make it easier for other developers to understand the changes and roll them back if something went wrong. 

##### Don't Commit Half-Done Work
* You should only commit code when a logical component is completed. 
* Split a feature‘s implementation into logical chunks that can be completed quickly so that you can commit often.

##### Test Your Code Before You Commit
* Test it thoroughly to make sure it really is completed and has no side effects as far as you can see

##### Write Good Commit Messages 
* See Good Commit Message Standard 👇

##### Follow branch strategy
* See [Git Branching Strategy](./git-branch-strategy.md)


## Good Commit Message Standard
### Why 
Git commit messages are more than just annotations, they document the evolution of a project. Clear and standardized messages provide valuable context, helping engineer understand what changed, why it changed, and how it affects the codebase. Writing informative commit messages is one of the most effective ways to communicate intent across a team and to yourself later.

### Structure
Usually, A commit message is a single sentence. and it not to be able to provide enough information about the context of the commit. 
A structured commit messages could help


```
<type>[optional scope]: <subject> # less than 50 characters

[optional body ~ description]     # multiple line, less than 72 characters per line

[optional footer ~ reference]     # multiple line, less than 72 characters per line
```

#### Conventional Commits
Type     | Explain
---------|---------
feat     | Introduce a new feature to the codebase
fix      | Fix a bug in the codebase
docs     | Create/update documentation
style    | Feature and updates related to styling
refactor | Refactor a specific section of the codebase
chore    | Regular code maintenance
test     | Add or update code related to testing
revert   | Revert previous commit

* __BREAKING CHANGE__: a commit that has a footer `BREAKING CHANGE:`, or appends a `!` after the type/scope.

### Information in commit messages
* Describe why a change is being made.
* How does it address the issue?
* What effects does the patch have?
* Do not assume the reviewer understands what the original problem was.
* Do not assume the code is self-evident/self-documenting.
* Read the commit message to see if it hints at improved code structure.
* The first commit line is the most important.
* Describe any limitations of the current code.
* Do not include patch set-specific comments.

### Example

```
fix(ingress): multiple device race condition 

Due to AOR allow only 1 contact lead to rate condition in case multiple
device which require AOR store atleast 3 devices contact

Refs: VOIP1234
```

```
chore(freeswitch): hiding software info in SDP

Change o & c username to `-` to secure with default value FreeSWITCH

Refs: VOIP1234 
```

### How
### Terminal

``` shell
git commit
``` 

* configure the default editor
```shell
git config --global core.editor <editor-name: "vim", "nano", "emacs">
```

### Visual Studio Code
* staging the change
* click commit button without message 
* link: [VS Code tips — Use an editor to write git commit messages](https://youtu.be/xGZ7OJYVFuY?feature=shared)

## Reference
* [Git Tips and Git Commit Best Practices](https://gist.github.com/luismts/495d982e8c5b1a0ced4a57cf3d93cf60)
* [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)
* [Best Practices for Git Commit Message | Baeldung on Ops](https://www.baeldung.com/ops/git-commit-messages)
* [How to Write Better Git Commit Messages – A Step-By-Step Guide](https://www.freecodecamp.org/news/how-to-write-better-git-commit-messages/)
