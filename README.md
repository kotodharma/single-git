Git was not designed for single-file projects, or managing multiple text files independently within a directory.
However, this shell script works around it by creating a unique bare repository for each file, using a Git command to set a different location for each file's `.git` directory.

# Instructions

Copy the script into a folder in `$PATH`, say as `~/bin/git1` (or `g1`), and mark it executable:

Use its `init` subcommand to create a bare repository for the target file (e.g., **foo.txt**).
Note that these commands are for the *script*, not for *git* itself:

```
  git1 foo.txt init
```

You should see git output indicating successful repo creation.
Perform this step only once, at the outset.
The repository is named using the prefix `.g1_` followed by the filename;
for instance, `.g1_foo.txt` for **foo.txt**.

To execute git commands for a specific file, use the script with the filename as the first argument, followed by standard git commands and options:

```sh
  git1 foo.txt status
  git1 foo.txt commit -m "added new blah"
  git1 foo.txt diff
  git1 foo.txt log
```

Since each bare repository is unique to its file, you can create multiple repositories in the same directory.
Always use the file name as the first argument to specify the repository for git commands.
Ensure you use this script within the directory containing both the file and its repository.

To remove a repository (this does not remove the tracked file):

```
 git1 foo.txt rm
```

To list existing single-file repositories in the current directory:

```
 git1 ls
```

Tip: For extensive git work on a file, create a temporary alias for `git1 foo.txt`:

```
 alias gg='git1 foo.txt'
```

Then, you can simplify commands: `gg diff`, `gg commit`, etc.

# Related

For ready use in Vim, see [single-file-git.vim](https://github.com/konfekt/single-file-git.vim/).

# Credits

This repo forked [David J. Iannucci's single-file-git](https://github.com/kotodharma/single-file-git) to whom all credit shall be due and all license restrictions be duly respected.
