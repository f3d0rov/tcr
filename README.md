# tcr
`tcr` is a "test &amp;&amp; commit || revert" utility tool written for bash.

It manipulates `git` in order to simplify commiting and reverting changes.

## Installation
`tcr` is a simple bash script. You can download it and use it directly via `./tcr`, or you can save it to the `/usr/local/bin` directory so that it would be avaliable from anywhere.

## Usage

The tool should be used from an initialized git repository. `tcr help` will print the list of available commands:
```
Available commands:
  ./tcr status                             - prints the current status of the TCR session.
  ./tcr start                              - starts a TCR session.
  ./tcr commit "<optional commit message>" - commits current changes.
  ./tcr revert                             - reverts current changes to the state of the last commit.
  ./tcr done                               - stops the current TCR session. Performs a soft reset to the initial commit.
  ./tcr merge "<optional commit message>"  - stops the current TCR session. Squashes the commited changes into a single commit.
```


The general workflow is as follows:

```bash
tcr start # Initialize a TCR session.

... # Introduce new changes to the repository

tcr commit # Commit all of the changes into a temporary commit

... # Introduce more changes

tcr revert # Revert all of the changes to the state of the last commit

tcr done # Stop the TCR session. Git will perform a soft reset to the initial commit 
         # (all of the made changes will be present as uncommited, unstaged changes to the initial commit)
```

You can also squash all of the commits made during the session together:

```bash
tcr merge "Updated stuff"
```

`tcr status` can be used to check the status of the session:
```bash
tcr status
```


## test && commit || revert
"test && commit || revert" is a programming workflow introduced by Kent Beck and Oddmund Strømme. It constitutes making small changes to the code that are then immediately commited if tests pass, and reverted otherwise. I recommend reading [Kent Beck's article on this methodology](https://medium.com/@kentbeck_7670/test-commit-revert-870bbd756864) if this sounds interesting.

