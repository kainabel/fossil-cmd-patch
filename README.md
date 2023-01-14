# Hello

In case anyone's really interested in reading this:

Just a little test to try out the behavior of the new [fossil git export](https://fossil-scm.org/index.html/doc/trunk/www/mirrortogithub.md) feature of [Fossil SCM](https://fossil-scm.org/).

Here is the *slightly* larger test version of the function by the author(s) himself, which mirrors the [source code](https://github.com/drhsqlite/fossil-mirror) of Fossil.

## Attention

The whole thing is actually only intended for storage and it cannot be ruled out that the behaviour of the then modified software will lead to undesired results.

*Check possible bugs in behavior* __with an unpatched version__ *of* `fossil` *before you report a bug at Fossil SCM.*

The latest __official versions__ of Fossil SCM: <https://fossil-scm.org/home/uv/download.html>

### Changes (updated for v2.20)

The diff contains a few changes for [Fossil SCM](https://fossil-scm.org/) and unravels the command input for ambiguous commands according to personal preferences.

The current default behavior of Fossil would be (which is pretty cool in itself):

```text
$ fossil cl
fossil: ambiguous command prefix: cl
fossil: could be any of: clean clean-glob clearsign clone close
fossil: use "help" for more information
```

#### Offical aliases in fossil are

Alias | Command
--- | ---
ci | commit
co | checkout
uv | unversioned
new | init

#### The new aliases are

Alias | Command | Ambiguous command prefixes in v2.20
--- | --- | ---
addrm | addremove | n/a
ch | changes | changes chat checkout cherry-pick
cl | clean |  clean clone close
de | descendants | deconstruct delete descendants describe detach
des | describe | descendants describe
ex | extras | export extras
in | info | info init interwiki
pool | stash | n/a
private | unpublished | n/a
re | revert |  rebuild reconstruct redo remote remote-url rename reparent revert
ss | stash | __ssl-config__
st | status | stash status
tgz | tarball | n/a
tkdiff | diff --tk | n/a
tl | timeline | __tls-config__
un | undo | undo unpublished unset unversioned

#### Further changes in behavior

The `diff` command can now also use `-u` for `--unified` and `-q` instead of `--brief`.

The `-h` switch for global use has been added to display the `help`.

> ### *Disadvantages*
>
> You must use the long form of option -h in the following commands:
>
> `--html` at commands: `help`, `wiki`
> `--versions` at command: `diff`
> `--dereference` at commands: `sha1sum`, `sha3sum`, `test-tarball`, `test-filezip`

The command call of `fossil stash` without further options now points to `fossil stash list` and not to `fossil stash save` as before.

The hidden test commands `test-grep` and `test-diff` are now more visible as ~~`fgrep`~~ `xgrep` and ~~`fdiff`~~ `xdiff` [default since v2.17](https://fossil-scm.org/home/info/9e330740ccfc6286) (and mainly intended as a help for Windows use). Wir hatten ja nichts.

Visible as 1st tier command (`fossil help`): tkdiff, pool, xgrep
Visible as 2nd tier command (`fossil help -x`): addrm, private, tgz

#### Comments

With this [commit](https://fossil-scm.org/home/file?ci=4b8efc05d7f70f9c&name=tools/mkindex.c&ln=33-52) the new method was introduced and described and is included in Release v2.20.
Thank you for this new feature among the other wonderful things.

### Other things from roadside

- [fnc](https://fnc.bsdbox.org/index): an interactive text-based user interface for [Fossil](https://fossil-scm.org)
  See also: [man fnc](https://fnc.bsdbox.org/uv/doc/fnc.1.html)

- [GWSL](https://opticos.github.io/gwsl) makes pretty windows when fossil runs on Windows in [WSL](https://learn.microsoft.com/en-us/windows/wsl/).

- The environment variable [FOSSIL_USER](https://fossil-scm.org/home/doc/trunk/www/env-opts.md) is useful to keep the name of the committer stable between machines and operating systems.
  For the commands `fossil init -A` (aka new) and `fossil clone -A` a different [admin user](https://fossil-scm.org/home/doc/trunk/www/caps/admin-v-setup.md) name should be specified with the -A option.

#### Usage (we all get old some day)

Go to the root directory of the source files and do something like that `patch -u -p 0 --dry-run < cmd-aliases.diff` for testing.

My currently preferred build options:
`./configure --disable-fusefs --json --with-openssl=auto --with-tcl=1 --with-tcl-private-stubs=1`
or
`./configure --disable-fusefs --json --with-openssl=auto`
or
nmake /f Makefile.msc FOSSIL_ENABLE_SSL=1 FOSSIL_ENABLE_JSON=1 FOSSIL_ENABLE_TCL=1 OPTIMIZATIONS=4 clean fossil.exe

See also:

- [Compiling and Installing Fossil](https://fossil-scm.org/home/doc/trunk/www/build.wiki)
- [Release Build How-To](https://fossil-scm.org/home/wiki?name=Release%20Build%20How-To)
- [How to build Fossil into OCI compatible containers](https://fossil-scm.org/home/doc/trunk/www/containers.md)

Reminder for me: If `patch` is not lying around under Windows, then [busybox](https://frippery.org/busybox/) or `wsl -e` is my friend.

Another way to get changes in (since v2.16): [`fossil patch`](https://fossil-scm.org/home/doc/trunk/www/patchcmd.md) and [`patch -h`](https://fossil-scm.org/home/help?cmd=patch)

- and (local) online as a [Windows Service](https://fossil-scm.org/home/doc/trunk/www/server/windows/service.md) `fossil winsrv create -P 8080 -S auto -R D:/Path/to/Repos --repolist` & `fossil winsrv start`
- and wide [fossil uv --help](https://fossil-scm.org/home/help?cmd=uv)
- [Althttpd with CGI](https://sqlite.org/althttpd/doc/trunk/althttpd.md)
