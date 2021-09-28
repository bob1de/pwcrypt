# pwcryptfs

```
Usage: pwcryptfs <subcommand>
   or: pwcryptfs {-h|--help}

This is a thin wrapper around the excellent gocryptfs program, which
allows to store sensitive data in an encrypted form inside a regular
file system directory.

It was originally created to securely store passwords, hence the name,
but you can of course throw any kind of files into the encrypted data
store, of which a cleartext view is mounted by fuse-based gocryptfs into a
temporary directory only the current user has access to.
Most notably, the data store created by this program is a regular
gocryptfs directory, meaning that you are not forced to use this wrapper
for working with it, should you decide to drop it one day.

After mounting the encrypted data store, a shell is started in the
mountpoint directory, allowing the user to work with the plain,
unencrypted view of the files in whatever way required.
When done and the shell was left, the data store is again unmounted
automatically so that no further access is possible.

The behavior can be tweaked in many ways by passing environment
variables. For instance, a different application (e.g. a graphical file
manager) can be started instead of the shell after mounting.

Options:
  -h, --help
    show this help and exit

Subcommands:
  init
    initialize a new data store (PWC_STORE must be absent or empty)
  mount (default)
    mount an existing data store and start a shell in the mountpoint
    directory
  passwd
    change password of an existing data store

Environment Variables:
  PWC_GCFS_INIT_OPTS (default: '-devrandom -scryptn 19')
    extra options to pass to gocryptfs when using the init subcommand
    to create a data store
  PWC_GCFS_MOUNT_OPTS (default: '')
    extra options to pass to gocryptfs when using the mount subcommand
  PWC_MOUNTPOINT
    if set, the mount subcommand will mount the data store to this
    directory rather than creating a temporary one
  PWC_POSTMOUNT_CMD (default: '$SHELL; clear')
    shell command(s) executed by the mount subcommand inside the
    mountpoint directory after mounting the data store
  PWC_STORE (default: '$HOME/.pwcryptfs-store')
    path to directory for storing encrypted files
```
