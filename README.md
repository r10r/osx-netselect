osx-netselect
=============

Switch network profiles on OSX from terminal.
Support for custom setup/teardown scripts.

**[me@foo]$ netselect w**

```bash
Switching network profile: Home -> Work
Password:
CurrentSet updated to 76809B31-F2D0-4872-A473-C0738AD282D2 (Work)
Added work route.
```

**[me@foo]$ netselect h**

```bash
Switching network profile: Work -> Home
Password:
CurrentSet updated to D28AC42A-7661-4FE1-B49F-63DA19FABF19 (Home)
Removed work route.
```

setup
-----------------------

* Copy [netselect](netselect) to somewhere in your path.
* Create folders for up and down scripts.

```bash
mkdir ~/.network/{up.d,down.d}
```

* Up and down script names must *match the network profile name*.
* See [example](example) how to set and remote a custom route.
* Up and down scripts are executed with root permissions using **sudo**

usage
-----------------------

### Available profiles

Let's say the following profiles are available:

```bash
[me@foo]$ scselect
Defined sets include: (* == current set)
   D28AC42A-7661-4FE1-B49F-63DA19FABF19	(Home)
   BDBFA23C-D3B9-4E43-9A18-C75C33259217	(Automatic)
 * 7C1E23D1-AB04-4C82-B0C1-05F1262BEAC6	(Home2)
```

### Pick a profile

**A** matches profile name **Automatic**:

```bash
[me@foo]$ netselect a
Switching network profile: Home2 -> Automatic
```

**home** matches **Home** exactly:
```bash
[me@foo]$ netselect home
Switching network profile: Home2 -> Home
```

### Errors

Ambigous selection: **ho** matches **Home** and **Home2**:

```bash
[me@foo]$ netselect ho
ERROR: Multiple profiles(#2) start with 'ho'.
-> Profile name must start with or equal pattern (case-inensitive).
-------------------------------------------------------------------
Defined sets include: (* == current set)
   D28AC42A-7661-4FE1-B49F-63DA19FABF19	(Home)
   BDBFA23C-D3B9-4E43-9A18-C75C33259217	(Automatic)
 * 7C1E23D1-AB04-4C82-B0C1-05F1262BEAC6	(Home2)
```


TODO
---------
* add bash completion for profile names
