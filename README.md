In case anyone's really interested in reading this:

# Hello
Just a little test to try out the behavior of the new [fossil git export](https://fossil-scm.org/index.html/doc/trunk/www/mirrortogithub.md) feature of [Fossil SCM](https://fossil-scm.org/).

Here is the *slightly* larger test version of the function by the author himself, which mirrors the [source code](https://github.com/drhsqlite/fossil-mirror) of Fossil.

## Attention
The whole thing is actually only intended for storage and it cannot be ruled out that the behaviour of the then modified software will lead to undesired results.

*Check possible bugs in behavior **with an unpatched version** of* `fossil` *before you report a bug at Fossil SCM.*

### Changes
The diff contains a few changes for [Fossil SCM](https://fossil-scm.org/) and unravels the command input for ambiguous commands according to personal preferences.

The current default behavior of Fossil would be:
```
$ fossil cl
fossil: ambiguous command prefix: cl
fossil: could be any of: clean clean-glob clearsign clone close
fossil: use "help" for more information
```

#### The new aliases are
#
Alias | Command
--- | ---
ch | changes
cl | clean
de | descendants
ex | extras
in | info
pool | stash
private | unpublished
re | revert
ss | stash
st | status
tgz | tarball
tl | timeline

#### Further changes in behavior
The `diff` command can now also use `-u` for `--unified` and `-q` instead of `--brief`.
The `-h` switch for global use has been added to display the `help`.

The command call of `fossil stash` without further options now points to `fossil stash list` and not to `fossil stash save` as before.

The hidden test commands `test-grep` and `test-diff` are now more visible as `fgrep` and `fdiff` (and mainly intended as a help for Windows use). Please use with caution.

#### Comments
Some new aliases have an asterisk behind them.
This prevents the listing of the main commands with 'fossil help'.
Try `fossil help -a` or `fossil help -x` to see the new aliases.
```
$ fossil help help
Usage: fossil help TOPIC
   or: fossil TOPIC --help

Display information on how to use TOPIC, which may be a command, webpage, or
setting.  Webpage names begin with "/".  To display a list of available
topics, use one of:

   fossil help                Show common commands
   fossil help -a|--all       Show both common and auxiliary commands
   fossil help -o|--options   Show command-line options common to all cmds
   fossil help -s|--setting   Show setting names
   fossil help -t|--test      Show test commands only
   fossil help -x|--aux       Show auxiliary commands only
   fossil help -w|--www       Show list of webpages
```

###### Usage (we all get old some day)
Go to the root directory of the source files and do something like that `patch -u -p 0 --dry-run < cmd-aliases.diff` for testing.

My currently preferred build options:
```
./configure --disable-fusefs --json --with-openssl=auto --with-tcl=1 --with-tcl-private-stubs =1
```

Reminder for me: If `patch` is not lying around under Windows, then [busybox](https://frippery.org/busybox/) is my friend.
