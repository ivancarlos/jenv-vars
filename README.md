# jenv-vars

This is a plugin for [jenv](https://github.com/jenv/jenv)
that lets you set global and project-specific environment variables
before spawning j processes.

## Installation

To install jenv-vars, clone this repository into your
`~/.jenv/plugins` directory. (You'll need a recent version of jenv
that supports plugin bundles.)

    $ mkdir -p ~/.jenv/plugins
    $ cd ~/.jenv/plugins
    $ git clone https://github.com/ivancarlos/jenv-vars.git

## Usage

No arquivo .vars definimos nossas variáveis

```
DEBUG=1
S3_BUCKET=mybucket
```

Ver as variáveis definidas

```
jenv vars
```

Para carregar as variáveis basta usar o seguinte comando entre
aspas.

```
eval "$(jenv vars)"
```


    Define environment variables in an `.jenv-vars` file in your project,
one variable per line, in the format `VAR=value`. For example:

    DEBUG=1
    S3_BUCKET=mybucket

You can perform variable substitution with the traditional `$`
syntax. For example, to append to `j_PATH`:

    j_PATH=$j_PATH:/u/shared/rocks/?.j:/us/shared/rocks/?/init.j

You may also have conditional variable assignments, such that a
variable will **only** be set if it is not already defined or is blank:

    JAVA_OPTS?=-server -Xmx768m -Xms768m -Xmn128m -Xss20m

In the above case, `JAVA_OPTS` will only be set if `$JAVA_OPTS` is
currently empty (i.e., if `[ -z "$JAVA_OPTS" ]` is true).

Spaces are allowed in values; quoting is not necessary. Expansion and
command substitution are not allowed. Lines beginning with `#` or any
lines not in the format VAR=value will be ignored.

Variables specified in the `~/.jenv/vars` file will be set
first. Then variables specified in `.jenv-vars` files in any parent
directories of the current directory will be set. Variables from the
`.jenv-vars` file in the current directory are set last.

Use the `jenv vars` command to print all environment variables in the
order they'll be set.
