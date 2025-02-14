# tgm-record

A couple scripts to assist in automatically recording, playing back and
encoding TGM2P sessions.

## Prerequisites
* A version of MAME that takes single-dash parameters. Or you can modify the script to use double-dash parameters.
* zenity for displaying the tag dialog in tgm-record if there is no terminal. Or you can just always run it in a terminal.
* ffmpeg with libx264 support enabled for encoding. Or you can modify the script to not use libx264.
* mplayer for searching for the last game in a record. Or you can just always encode the entire session and manually trim it or whatever.
* On macOS, you might need to set up mame.ini manually before MAME will work; [I've prepared some template mame.ini files in another repository to help you get up and running.](https://github.com/nightmareci/macos-mame-ini)

## Preparation
1. Set the MAMEROOT environment variable, or change mameroot at the top of each script.
2. Tweak the tgm-launcher script to launch your games with the appropriate parameters. By default it supports tgm2p and tgmj without extra parameters.
3. Modify the script in any additional ways required by the prerequisites above. If you already fulfil the prerequisites, you probably don't need to change anything here.

## Usage
1. Run tgm-record with the game name (e.g. tgm2p, tgmj) to play a game. Example: `$ tgm-record tgm2p`
2. When you quit MAME, you will be asked to "tag" the record, or discard it. Example tag: `> death_gm`
3. Each tagged record will also have the date and time in its filename.
4. The latest discarded record is also kept, just in case.
5. To play back, run tgm-playback with the game name. Example: `$ tgm-playback tgm2p`
6. It will list the recorded sessions available.
7. Specify a record to play back. Tab-completion works.
8. Answer any other questions it asks.
9. The rest is entirely automated; it will run MAME, stop it when the input is finished, and process and encode the output.
10. You can use tgm-delete with the game name to delete a saved record. Example: `$ tgm-delete tgmj`

## Notes
Unfortunately, MAME refuses to dump an AVI into a FIFO, so you must
have enough space for the entire AVI file of the session you are playing back,
which can be several gigabytes for long sessions. This is true even if you are
only saving the last game, as that only affects the encoding phase. It is thus
recommended that you restart MAME every couple of games to keep the records
short.

Hopefully this can be resolved at some point.
