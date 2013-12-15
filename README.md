# lua-linenoise - Lua binding for the linenoise command line library

[linenoise](https://github.com/antirez/linenoise) is a delightfully simple command line library.

[lua-linoise](https://github.com/hoelzro/lua-linenoise) is a lua module is simply a binding for linenoise.

This module is a refactoring of the lua-linenoise for compatibility with [LuaDist](luadist.org).

# Instalation

You must have luadist installed.

```bash
$ git clone https://github.com/nuxlli/lua-linenoise
$ luadist make lua-linenoise
```

# Usage

This library is a fairly thin wrapper over linenoise itself, so the function calls
are named similarly.  I may develop a "porcelain" layer in the future.

## L.linenoise(prompt)

Prompts for a line of input, using *prompt* as the prompt string.  Returns nil if
no more input is available.

## L.historyadd(line)

Adds *line* to the history list.

## L.historysetmaxlen(length)

Sets the history list size to *length*.

## L.historysave(filename)

Saves the history list to *filename*.

## L.historyload(filename)

Loads the history list from *filename*.

## L.clearscreen()

Clears the screen.

## L.setcompletion(callback)

Sets the completion callback.  This callback is called with two arguments:

  * A completions object.  Use L.addcompletion to add a completion to this object.
  * The current line of input.

## L.addcompletion(completions, string)

Adds *string* to the list of completions.

All functions return nil on error; functions that don't have an obvious return value
return true on success.

# Example

```lua
local L = require 'linenoise'
-- L.clearscreen()
print '----- Testing lua-linenoise! ------'
local prompt, history = '? ', 'history.txt'
L.historyload(history) -- load existing history
L.setcompletion(function(c,s)
   if s == 'h' then
    L.addcompletion(c,'help')
    L.addcompletion(c,'halt')
  end
end)
local line = L.linenoise(prompt)
while line do
    if #line > 0 then
        print(line:upper())
        L.historyadd(line)
        L.historysave(history) -- save every new line
    end
    line = L.linenoise(prompt)
end
```