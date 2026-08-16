FORK CUBED! Fork of FozzTexx's fork of Jim Brain's tcpser program, adding some convenience features for my own purposes, figured I'd share.

So here's what I'm working on:

- [ ] ~~I/O via stdio~~<sup>1</sup>

- [x] AT&H for help with AT commands and S registers

- [ ] outbound SSH connections<sup>2</sup>

- [ ] Adding listeners in command mode

- [ ] Adding lookup phonebook entries in command mode, stored in a file, and somehow still retain compatability with -n



---

<sup>1</sup> Ngl, this was proving to be WAY more involved than I could handle at the time, so I opted to abuse "-v" as a shortcut and will probably never do this (see [STDIO.md](STDIO.md)).

<sup>2</sup> Assuming I can accomplish this, I expect inbound connections are going to be twice as hard, so I'm probably not going to bother.




