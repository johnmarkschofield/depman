depman
======

Dependency Manager for Linux


## Introduction 

Why do you need a dependency manager?

* Some private data centers do not permit unlimited outbound internet for security reasons
* Some organizations want to audit all packages installed on their servers; pulling packages from upstream remote sources makes that impossible.
* Even if you specify a Python Package version number in your requirements.txt, that particular package version may cease to become available at the upstream source.
* Due to network issues or server problems, many upstream sources are temporarily unavailable. If you have an urgent need to deploy a new instance, that's a problem.

Depman manages your dependencies for you.

NOTE: At present, depman only handles apt packages and repos. Adding Python Packages (pip), Ruby Gems, and RedHat (yum) packages and repos are on the roadmap.

## Usage

```
$ depman update
# updates pip, gem, apt CURRENT repo from upstream sources.
```

The "current" repo is the only pre-existing repo in depman, and the "update" command updates it from the upstream repos. You can edit your /etc/apt/sources.list to point to the current repo, and this is effectively the same as pointing to upstream. (Except that the current repo is updated only when the "depman update" command is run.)

```
$ depman create FOO
# creates a new empty repo
```


```
$ depman promote current foo
# promotes all packages in current apt, pip, gem to foo repo.
```

```
$ depman delete foo
# deletes foo repo
```

```
$ depman promote current foo --package=tzdata --version=1.2.3
# promotes version 1.2.3 of package tzdata from current repo to foo repo.
```

```
$ depman diff current foo
# display differences between current repo and foo repo
```

```
$ depman mirror http://depman.rackspace.com
# Make current depman server a mirror of the specified upstream depman repo.
# Good for clients who want a complete mirror on their local network so they can audit it.
```

```
$ depman mirror http://depman.rackspace.com FOO
# same as above, but only update FOO repo.
```

```
depman showconfig foo
# Display instructions for how to config a system to connect to the foo repo on the depman server.
```
