# PLTG-Hart

Programming language for the [PLT Games December 2012 competition](http://www.pltgames.com/competition/2012/12).

This is a simple implementation of a 2-state, 3-symbol Turing machine. The symbols are `W`, `R`, and `H`. They may be run-length encoded. EG, `WWWRRWWWH` can be written `3W2RWWW1H`. The language is case-insensitive, whitespace between symbols is ignored (whitespace between digits, or between a number and the symbol it precedes, is a syntax error), and comments extend from any non-digit, non-`WRH` character to the end of the line.

The first line of the file indicates the starting tape position (0-based), the initial state, and the (optional) encoding to use for the output of the final state. The rest of the file is the initial tape contents.

The rules for the machine are as follows:

|val|state|new val|new state|shift|
|---|-----|-------|---------|-----|
|W|A|R|B|→|
|W|B|H|A|←|
|R|A|H|A|←|
|R|B|H|B|→|
|H|A|R|A|←|
|H|B|W|A|→|

The program ends when the position moves past either end of the tape.

The final state is interpreted as trinary (W, R, and H map to 0, 1, and 2, respectively), and then displayed based on the provided encoding. The encoding can be either a base (in decimal) for numeric output, the name of a character encoding, `WRH` for source encoding, or `RLE` for run-length encoded source. The default is `12` for duodecimal output (since it's [the best base](http://en.wikipedia.org/wiki/Duodecimal)).

Assuming a program ends with the state RRHHRRH (interpreted as 1122112 in ternary) here is a list of potential outputs:
* 2:       00000100 10110010
* 3:       1122112
* 10:      1202
* 12:      842 (the default)
* 16:      4B2
* ASCII:   -ERROR-
* Latin-1: EOT      ²
* UTF-8:   -ERROR-
* UTF-32:  ұ
* WRH:     RRHHRRH
* RLE:     2R2H2RH
