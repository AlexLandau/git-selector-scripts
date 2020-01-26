# git-selector-scripts
Bash functions `gs` and `gg` for selecting files from `git status` using line numbers.

* `gs`: Prints `git status` with line numbers.
* `gg [line-numbers] [command]`: Runs the given command, passing the files on the given line numbers as arguments.

# Example usage

```
$ gs
1  On branch master
2  Your branch is up-to-date with 'origin/master'.
3  Untracked files:
4    (use "git add <file>..." to include in what will be committed)
5
6       newfile1
7       newfile2
8       newfile3
9       newfile4
10      newfile5
11
12  nothing added to commit but untracked files present (use "git add" to track)

$ gg 6,8-10 git add
Running git add  "newfile1" "newfile3" "newfile4" "newfile5"

$ gs
1  On branch master
2  Your branch is up-to-date with 'origin/master'.
3  Changes to be committed:
4    (use "git reset HEAD <file>..." to unstage)
5
6       new file:   newfile1
7       new file:   newfile3
8       new file:   newfile4
9       new file:   newfile5
10
11  Untracked files:
12    (use "git add <file>..." to include in what will be committed)
13
14      newfile2

$ gg 7,9 git reset HEAD
Running git reset HEAD  "newfile3" "newfile5"

$ gs
1  On branch master
2  Your branch is up-to-date with 'origin/master'.
3  Changes to be committed:
4    (use "git reset HEAD <file>..." to unstage)
5
6       new file:   newfile1
7       new file:   newfile4
8
9  Untracked files:
10    (use "git add <file>..." to include in what will be committed)
11
12      newfile2
13      newfile3
14      newfile5

$ gg 12-14 rm
Running rm  "newfile2" "newfile3" "newfile5"

$ gs
1  On branch master
2  Your branch is up-to-date with 'origin/master'.
3  Changes to be committed:
4    (use "git reset HEAD <file>..." to unstage)
5
6       new file:   newfile1
7       new file:   newfile4
```

# How to install

This is implemented as a Bash function, not an executable. The installation process is accordingly manual. Note that, as a rule of thumb, you shouldn't install things in the way I'm recommending here unless you trust the source, for security reasons.

Download the `.define_gs_and_gg` file and put it in your home directory (`~`). Then add the following line to your `.bashrc` or `.bash_profile` file, as appropriate:

`source ~/.define_gs_and_gg`

You will need to `source` the modified file or close and re-open your terminal for the commands to become available.

# Troubleshooting

If you have existing aliases for `gs` or `gg`, those will take precedence over these functions. You will need to remove those aliases and re-open the terminal to use these.
