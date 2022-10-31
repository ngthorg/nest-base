# Git Conventional

## Introduce

- git commit convention
- git branch convention
- set up `commitlint` with husky
- set up `validate-branch-name` with husky

## git commit convention

### Commit Formats

Default

<pre>
<b><a href="#types">&lt;type&gt;</a></b></font>(<b><a href="#scopes">&lt;optional scope&gt;</a></b>): <b><a href="#subject">&lt;subject&gt;</a></b>
</pre>

Merge

<pre>
Merge branch '<b>&lt;branch name&gt;</b>'
</pre>

## git branch convention

-
-

## set up `commitlint` with husky

```bash
# Install commitlint cli and conventional config
npm i -D @commitlint/cli @commitlint/config-conventional
```

```yaml
# .commitlintrc.yml
# Configure commitlint to use conventional config
extends: ['@commitlint/config-conventional']
```

To lint commits before they are created you can use Husky's commit-msg hook:

```bash
npx husky-init
```

```bash
npx husky add .husky/commit-msg 'npx --no -- commitlint --edit "$1"'
```

## set up `validate-branch-name` with husky

```bash
# Install validate-branch-name
npm i -D validate-branch-name
```

```yaml
# .validate-branch-namerc.yml
# Configure pattern and errorMsg
pattern: "^(master|main|develop){1}$|^(feature|fix|hotfix|release)\/.+$"
errorMsg: 'Branch name validate failed please rename your current branch'
```

Define pre-commit file under .husky direcotory.

```bash
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npx validate-branch-name
npm run lint
```
