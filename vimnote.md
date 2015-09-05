# Usefull but don`t know `vim` command

1. `dw`,delete a work
2. `d$`,delete end of the line
3. `r{x}`,replace the charactor at the cursor with {x}
4. `ce`,change until end of a word,and change `INSERT` mode
5. `CTRL+R`,show location in the file and file status
6. `CTRL+O`,go back to where you came from
7. `CTRL+I`,repeat to go back further
8. `%`,to find a matching ),], or } . **
9. `?`,followed by a phrase searches BACKWARD for the phraseng.
10. `/`,followed by a phrase searches FORWARD for the phraseng.
11. `:s/old/new`,to substitute new for the first old in a line type
12. `:s/old/new/g`,to substitute new for all `old`s on a line type
13. `:#,#s/old/new/g`,to substitute phrases between two line #`s type
14. `:%s/old/new/g`,to substitute all occurrences in the file type
15. `:%s/old/new/gc`,to ask for confirmation each time add `c`
16. `:r FILENAME`,insert the contents of a file
17. You can also read the output of an external command.  For example,
    :r !ls  reads the output of the ls command and puts it below the cursor
18. `R`,a capital R to replace more than one word
19. Typing ":set xxx" sets the option "xxx".  Some options are:
    `ic` `ignorecase`       ignore upper/lower case when searching
    `is` `incsearch`        show partial matches for a search phrase
    `hls` `hlsearch`        highlight all matching phrases
    You can either use the long or the short option name.
    Prepend "no" to switch an option off:   `:set noic`
20. `CTRL-D`,to see possible completions
