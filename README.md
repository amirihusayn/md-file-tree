# md-file-tree by [@michalbe](http://github.com/michalbe)

Generate markdown tree of all the files in a directory, recursively.

## Manual use

### 1- Install the script

```bash
npm install md-file-tree -g
```

### 2- Run the tree script in any directory

```bash
md-file-tree
```

## Use as Github Action  

Add `.github/[your-action-name].yml` inside your repository with following content:  

```yml
on: [push]

jobs:
  create_md_file_tree_job:
    runs-on: ubuntu-latest
    name: A job to create file tree
    steps:
      - name: checkout latest commit 
        uses: actions/checkout@v3
      - name: generate markdown file tree
        uses: actions/md-file-tree@v0.3.0
        with:
          file-name: 'list' # The name of generated file
          input-path: './' # The path which you want its tree
          output-path: './' # The output path that generated file will be commited there
      - name: Save file tree
        uses: stefanzweifel/git-auto-commit-action@v4
        with:
          commit_message: Add generated tree
```

## Options  

### Enable emoji (📂 & 📄) with the command line switch

```bash
md-file-tree --emoji
md-file-tree -e
```

### Redirect the output to a file

```bash
md-file-tree > list.md
```

This generates the `list.md` file with:

```markdown
- __michal__
  - [LICENSE](LICENSE)
  - [README.md](README.md)
  - __bin__
    - [cli.js](bin/cli.js)
  - [michal.png](michal.png)
  - [node\_modules](node_modules)
  - [npm\-debug.log](npm-debug.log)
  - [package.json](package.json)
  - [screen.png](screen.png)
  - __scripts__
    - [assert.js](scripts/assert.js)
    - [fancom.js](scripts/fancom.js)
    - [jshintrc.js](scripts/jshintrc.js)
    - [package\-json.js](scripts/package-json.js)
    - [precommit\-hook.js](scripts/precommit-hook.js)
    - [scripts.js](scripts/scripts.js)
    - [tests.js](scripts/tests.js)
  - __tests__
    - [michal\-tests.js](tests/michal-tests.js)
```

## Hidden files & directories

Please note that this script __skips__ all hidden files and directories (with `.`, like `.git` or `.gitignore`) &
 the contents of the `node_modules` directory.
