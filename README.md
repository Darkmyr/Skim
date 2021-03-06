# Skim

Skim is an alternative to wix/wml or symlinks for use in real time development of dependencies.

In simple terms, it watches a directory and copies its contents to a new directory

### Installation

Install [fswatch](https://github.com/emcrisostomo/fswatch) (`brew install fswatch`)

Place Skim (below) in your `.bash_profile` or `.zshrc`

```sh
function skim() {
  function run_rsync() {
    rsync -rtuv "$1" "$2" --exclude "node_modules" --exclude ".git"
  }
  run_rsync "$1" "$2";
  fswatch -o $1 | while read f; do run_rsync "$1" "$2"; done;
}
```

run `source <path/to/your/.bash_profile/or/.zshrc>`

### Usage

Basic Usage:
```sh
skim old_dir/ new_dir
```

Note the `/`. it matters

### Limitations 

Skim currently only supports one directory (or package) per process at this time. 
