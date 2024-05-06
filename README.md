# harper
Command-line utility for monitoring and controlling MPRIS-compatible music/media players.  

Primarily for use with polybar and other desktop tools.

___This tool is in the early design phase and is not currently functional.___

### Why

I started this project because use [mihirlad55's](https://github.com/mihirlad55) 
polybar-spotify module. Breaking changes in polybars IPC methodology resulted in 
me [jumping into his codebase](https://github.com/corigne/polybar-spotify-module) 
and learning a bit about dbus, mpris, and polybar.

I was initially going to utilize the playerctl library, 
but the project hasn't had much activity in the last few years.
 
### Project Goal

The goal of this project is to provide a fast and lightweight daemon for 
monitoring and controlling mpris media players.

One of the downsides to a tool like polybar-spotify is that it is coupled with 
it's subsribing end-user technology.

Instead, I wanted a utility that can provide information and register blocking 
callbacks, like playerctl, but could also be configured with a series of 
non-blocking callbacks that could be configured at runtime by the user.

For example, harper could be configured at runtime either by configuration file 
or shell-commands to specific shell commands when a specific mpris signal is 
detected.  A user could then call `harper --player=spotify,vlc --action=play` 
`polybar-msg polybar-harper play` when a song starts playing on the tracked 
players, specificed as spotify or vlc, in this instance. On the polybar side, 
a user could then customize the specific behavior desired from polybar, perhaps 
calling `harper status` from the polybar-module to update the current track 
status.

While playerctl does work for this usecase when accessed via a shell script or C 
program, like polybar-spotify, the playerctl --follow commands are strictly 
blocking, and the official library interface are in C and Python.

I thought that developing this daemon could provide some useful utility, even
beyond my general usecase.

### TODO

1:1 or nearly 1:1 parity with playerctl.

1. mpris player functionality (detect, get info from, control playback)
2. unicode player icon retreival for common players
3. blocking status update hooks (similar to --follow in playerctl)
4. non-blocking status update callbacks, one-time callback, continuous callback, callback management (listing and removal)
5. smart player selection
6. player filtering
7. scrolling status info
8. optional systemd service integration
