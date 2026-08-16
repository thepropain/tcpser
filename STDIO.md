The code for hardware line emulation and twiddling was infuriating to work with, so I figured out a sub-optimal shortcut using tcpser's TCP mode for VICE (-v). This mode does some special escape sequencing to control the emulated hardware lines by sending 2 bytes: 0xFF and a data byte. In order to be sure nothing I did accidentally twiddled tcpser's lines, I banged out a filter for any 0xFF bytes:

`#include <stdio.h>
#include <unistd.h>`

`int main(void) {
    unsigned char ch;
    while (read(STDIN_FILENO, &ch, 1) > 0) {
        if (ch == 0xFF) {
            unsigned char dbg[2] = {0xFF, 0xFF};
            write(STDOUT_FILENO, dbg, 2);
        } else {
            write(STDOUT_FILENO, &ch, 1);
        }
    }
    return 0;
}`

Save as escape255.c, then compile with:

`gcc -O2 escape255.c -o escape255`

Now you need two terminals. In one, run this:

`tcpser -v 25232`

And in the other:

`socat STDIO,raw,echo=0 SYSTEM:"./escape255 | nc localhost 25232"`



To get out of this, hit the tcpser terminal with a <CTRL-C>, then "killall socat". You'll probably want to go ahead and close the socat terminal, cos it acts funny after this.
