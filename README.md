# SmartWatch

SmartWatch is an alternative to wml or symlinks for use in real time development of dependencies.



### Installation

Install fswatch (`brew install fswatch`)

Place smartwatch (below) in your `.bash_profile` or `.zshrc`

```sh
function smartwatch() {
  function run_rsync() {
    rsync -rtuv "$1" "$2"
  }
  run_rsync "$1" "$2";
  fswatch -o $1 | while read f; do run_rsync "$1" "$2"; done;
}
```

### Usage

Basic Usage:
```sh
smartwatch old_dir/ new_dir
```

### Limitations 

Smartwatch currently only supports one directory (or package) per process at this time. 
