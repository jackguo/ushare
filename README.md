GeeXboX uShare (Modified Version)
================================================

GeeXboX uShare is a UPnP (TM) A/V Media Server. It implements the server
component that provides UPnP media devices with information on available
multimedia files. uShare uses the built-in http server of libupnp to
stream the files to clients.

GeeXboX uShare is able to provide access to both images, videos, music
or playlists files (see below for a complete file format support list).
It does not act as an UPnP Media Adaptor and thus, can't transcode
streams to fit the client requirements.

uShare is written in C for the GeeXboX project (see http://www.geexbox.org/).
It is designed to provide access to multimedia contents to GeeXboX but can of
course be used by any other UPnP client device.

This is a modified version of the original release. Including some bug fixes and modifications in order to compile and run on **FreeBSD**. See *ChangeLog* for details. For the remaining part of the document, if not explicitly speciifed, it's assumed that the underlying os is a FreeBSD system. Some additional settings  might be necessary if it would be  used on linux systems. See section **For Linux Users**.

GeeXboX uShare is free software - it is licensed under the terms of the GNU
General Public License (GPL).

Homepage (the original release)
================================

Web site and file area for uShare is hosted on GeeXboX server :

   http://ushare.geexbox.org/

The latest version of uShare should always be available on this site.

Requirements
============

The following programs are required to build uShare:

 * GNU Make

   GNU Make is a tool which controls the generation of executables and other non-source files of a program from the program's source files
   webpage: https://www.gnu.org/software/make/

 * pkg-config.

   pkg-config is a helper tool used when compiling applications and libraries.
   It helps you insert the correct compiler options on the command line.
   (see http://pkg-config.freedesktop.org/wiki/ ).

The following UPnP library is required to build and run uShare :

 * libupnp, 1.4.2 or later

   The libupnp library is used to communicate using the UPnP protocol.
   libupnp can be downloaded from http://pupnp.sourceforge.net/.

The following DLNA library is required for proper DLNA support :

 * libdlna, 0.2.1 or later

   The libdlna library is used to provides DLNA profiles informations.
   libdlna can be downloaded from http://libdlna.geexbox.org/.

Building and Installation
=========================

Compile uShare by running configure and then make. This should
produce an executable ushare in the src subdirectory, which can be
used right away. No extra files need to be installed.

You can pass the CFLAGS you want to configure including -DDEBUG in order
to activate support for debug messages in uShare.

Example :

CFLAGS="-Os" ./configure --prefix=/usr
gmake

You can enable DLNA support by doing a:
./configure --enable-dlna

If you want to install uShare on your system, run :

gmake install-strip

This will copy the executable and manual page into their appropriate
directories (/usr/bin and /usr/man/man1 in this example).

For more information regarding configure and make, see the INSTALL document.

Usage
=====

uShare runs from the console only. It supports the usual --help option
which displays usage and option information.

Usage: ushare [-n name] [-i interface] [-c directory] [[-c directory] ...]
Options:
 -n, --name=NAME        Set UPnP Friendly Name (default is 'uShare')
 -i, --interface=IFACE  Use IFACE Network Interface (default is 'eth0')
 -f, --cfg=FILE         Config file to be used
 -p, --port=PORT        Forces the HTTP server to run on PORT
 -q, --telnet-port=PORT Forces the TELNET server to run on PORT
 -c, --content=DIR      Share the content of DIR directory.
 -w, --no-web           Disable the control web page (enabled by default)
 -t, --no-telnet        Disable the TELNET control (enabled by default)
 -o, --override-iconv-err       If iconv fails parsing name, still add to media contents (hoping the renderer can handle it)
 -v, --verbose          Set verbose display
 -x, --xbox             Use XboX 360 compliant profile
 -d, --dlna             Use DLNA compliant profile (PlayStation3 needs this)
 -D, --daemon           Run as a daemon.
 -V, --version          Display the version of uShare and exit
 -h, --help             Display this help

uShare gets its configuration from the /etc/ushare.conf file.
You can force configuration options through command line.

uShare expects one or several directory argument (-c argument),
specifying where multimedia files are stored. You should probably also use
the -i option to specify which interface uShare should listen on.

   ushare -c /shares
   ushare -c /shares1 --content=/shares2

You can also perform remote control of uShare UPnP Media Server through its
web interface. This let you define new content locations at runtime or
update the currently shared one in case the filesystem has changed.
Just go to :

   http://ip_address:port/web/ushare.html

See the manual page for more details :

   man ushare

Supported File Formats List
===========================

- Video files : asf, avi, dv, divx, wmv, mjpg, mjpeg, mpeg, mpg, mpe,
                mp2p, vob, mp2t, m1v, m2v, m4v, m4p, mp4ps, ts, ogm, mkv,
                rmvb, mov, qt

- Audio files : aac, ac3, aif, aiff, at3p, au, snd, dts, rmi, mp1, mp2, mp3,
                mp4, mpa, ogg, wav, pcm, lpcm, l16, wma, mka, ra, rm, ram

- Images files : bmp, ico, gif, jpeg, jpg, jpe, pcd, png, pnm, ppm,
                 qti, qtf, qtif, tif, tiff

- Playlist files : pls, m3u, asx

If you want uShare to support more file formats, simply add its properties
in the src/mime.c table. Do not forget to send a patch to update uShare.

Known bugs and limitations
==========================

If you need to listen on more than one interface, you will have to start
multiple instances of the media server.

uShare keeps some information on files in memory.
If your multimedia collection is huge, this might be a problem.

For Linux Users
===============

The source code should just work on any Linux os as it does on FreeBSD systems. But the default settings in `configure` script is meant to work only for FreeBSD, Linux users need to speficy the compiler (via `CC`) and make system (via `MAKE`) accordingly.In the usual case, Gcc is the default comiler and gnu make is the default make system on linux.

For example:
```C
CC=gcc MAKE=make ./configure ...
```

Also, since the `make` command on linux is default to be gnu make, all the `gmake` commands mentioned above should be replaced with `make`.

Trademarks
==========

UPnP(TM) is a trademark of the UPnP(TM) Implementers Corporation.

-
