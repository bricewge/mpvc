# mpvc

An mpc-like control interface for mpv with a nearly complete compatibility layer for mpc commands in
addition to GNU-style arguments. [Check out the mpc manpage for details.](http://linux.die.net/man/1/mpc)

![ExampleOutput](https://github.com/Wildefyr/mpvc/blob/master/output.png)

## Dependencies

Required:

- `mpv`
- `socat` / `nc`: `socat` preferred due to the differing implementations of netcat across UNIXes.
- `seq` / `jot`
- A sane version of `awk`

Optional:

- `bc`: For changing playback speed.
- soonTM: `youtube-dl` to download media for playback

## Install

If you have packaged mpvc for your distribution, let me know so I can add it here.

Distribution Packages:
- [Arch](https://aur.archlinux.org/packages/mpvc-git) - `pacaur -y mpvc-git`
- [Gentoo](https://gitlab.com/xy2_/osman) - `emerge mpvc`
- [Nixos](http://github.com/nixos/nixpkgs) - `nix-env -i mpvc`

To manually install mpvc, use the Makefile provided or link/copy mpvc to somewhere to your $PATH.

## Usage

mpvc requires the use of mpv and its `--input-ipc-server` option.

mpvc automatically opens an ipc-server for you when adding files to be played,
but by default will close the ipc-server when all files have finished playing.

To keep the ipc-server open permanently, use:
```
$ mpv --input-ipc-server /tmp/mpvsocket
```

## Useful Tricks

- Hotkey daemons like [sxhkd](https://github.com/baskerville/sxhkd)
  can be used to bind mpvc commands to key combinations. Alternatively check
  your window manager documentation on how to bind keys to commands.
- Any URL that is resolvable by mpv and/or youtube-dl can be added to the
  playlist, e.g. using [mps-youtube](https://github.com/mps-youtube/mps-youtube)
  with `player` set to mpvc and `playerargs` set to add. Further improvements to
  downloading URLs via youtube-dl
- mpvc GNU options can be combined together to give improved results: `$ mpvc -P -j 1`
  will make mpvc always start playing when switching to the next track.
- Piping files directly into mpvc is possible and preferable when
  loading multiple directories to be played:
```
$ find . type -f | mpvc
```
- You can use m3u playlists with mpv by saving the absolute path of your media into a file:
```
$ find "$(pwd)" -iname "*Your Artist Here*" > Artist.m3u
$ cat Artist.m3u | mpvc add
```

## Limitations

Like any piece of software, mpvc is not perfect:

- mpvc does not resolve individual files in a directory unless it is
  currently in or has been inside that directory, giving misleading results about
  the total number of files in the current playlist. This is a limitation of mpv.
- mpvc depends on shell tools. If your shell is misconfigured or you are using
  unusual variants of basic unix tools, mpvc is not guaranteed to work. However,
  all effort has been made to make mpvc as POSIX compliant as possible.

Check out the [Issue Tracker](https://github.com/wildefyr/mpvc/issues) for
further improvements to be made.
