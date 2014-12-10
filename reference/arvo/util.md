#[`:begin`](#begin)

`~zod/try=> :begin [~ship-name [~valid-ticket-for-ship]]`

Start a ship. `:begin` collects all of the necesarry information to start an Urbit ship. Takes an option `[~ship-name]` or `[~ship-name [~valid-ticket-for-ship]]` pair.

---

#[`:cat`](#cat)

`~zod/try=> :cat path-to-file [...]`

"cat" a file. `:cat` either prints a file, or concatenates and then prints multiple files to the terminal.
---

#[`:cp`](#cp)

`~zod/try=> :cp /path/to/source /path/to/destination`

Copy a file to a given location.

---

#[`:grep`](#grep)

`~zod/try=> :grep 'literal' `

"grep" a file or standard input. Currently only supports literals, but will eventuall support regular expressions.

----

#[`:hi`](#hi)

`~zod/try=> :hi ~ship ["message"]`

Send a ship a message which is empty by default, becoming their neighbor in the process. Often used to ping ships to check connectivity.

---

#[`:into`](#into)

`~zod/try=> :into /path/to/file 'contents'`

Write text to a file. If the specified file does not exist, create a file by that name.

---

#[`:ls`](#ls)

`~zod/try=> :ls path/to/directory`

"ls". List files at a path. Unlike "ls" in Unix, the current path `%` must be explicitly given (you cannot call `:ls` with no arguments to display the files at the current path).
---

#[`:mv`](#mv)

`~zod/try=> :mv /path/to/source /path/to/destination`

Move a file to a given location, creating a new revision of the source that omits the moved file.

---

#[`:reload`](#reload)

`~zod/try=> :reload %vane-name [...]`

Reload the standard library (zuse) and/or arvo vanes. If zuse is reloaded, vanes depending on the changes must be reloaded as well. For example `:reload %zuse %ford` is necessary to make use of changes in application code or the REPL.

---

#[`:rm`](#rm)

`~zod/try=> :cp /path/to/source`
---

#[`:solid`](#solid)

:solid "compile kernel"

---

#[`:sync`](#sync)

---

#[`:ticket`](#ticket)

---

#[`:unsync`](#unsync)

---

#[`:verb`](#verb)

---

#[`:ye`](#ye)

---