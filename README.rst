****************************
Mopidy-Tidal
****************************

.. image:: https://img.shields.io/pypi/v/Mopidy-Tidal.svg?style=flat
    :target: https://pypi.python.org/pypi/Mopidy-Tidal/
    :alt: Latest PyPI version

.. image:: https://img.shields.io/pypi/dm/Mopidy-Tidal.svg?style=flat
    :target: https://pypi.python.org/pypi/Mopidy-Tidal/
    :alt: Number of PyPI downloads

Tidal music service integration.

Installation
============

Install by running::

    pip install Mopidy-Tidal
    or
    pip3 install Mopidy-Tidal

In case you are upgrading your Mopidy-Tidal installation from the latest git sources, make sure to do a force upgrade from the source root::

    sudo python3 setup.py install --force


Python-Tidal
=============
Mopidy-Tidal requires the Python-Tidal API to function. This is usually installed automatically.
In some cases, Python-Tidal stops working due to Tidal changing their API keys.

When this happens, it will usually be necessary to upgrade the Python-Tidal API plugin manually ::

    sudo pip3 install --upgrade tidalapi

After upgrading tidalapi, it will often be necessary to delete the existing json file and restart mopidy.
The path will vary, depending on your install method::

    rm /var/lib/mopidy/tidal/tidal-oauth.json

Dependencies
=============
When using High and Low quality, be sure to install gstreamer bad-plugins, eg. ::

    sudo apt-get install gstreamer1.0-plugins-bad

This is mandatory to be able to play m4a streams.

Configuration
=============

Before starting Mopidy, you must add configuration for
Mopidy-Tidal to your Mopidy configuration file, if it is not already present.

The configuration is usually stored in `/etc/mopidy/mopidy.conf` or possibly `~/.config/mopidy/mopidy.conf`, depending on your system configuration ::

    [tidal]
    enabled = true
    quality = LOSSLESS
    #client_id =
    #client_secret =


Quality can be set to LOSSLESS, HIGH or LOW. Hi_RES(master) is currently not supported.
Lossless quality (FLAC) requires Tidal HiFi Subscription.

Optional: Tidal API `client_id`, `client_secret` can be overridden by the user if necessary.

OAuth Flow
=================

Using the new OAuth flow, you have to visit a link to connect the mopidy app to your login.

1. When you restart the Mopidy server, check the latest systemd logs and find a line like::

    journalctl -u mopidy | tail -5
    ...
    Visit link.tidal.com/AAAAA to log in, the code will expire in 300 seconds``

2. Go to that link in your browser, approve it, and that should be it.

Note that the login process is a **blocking** action, so Mopidy will not load until you approve the application.
The OAuth session will be reloaded automatically when Mopidy is restarted. It will be necessary to perform these steps again if/when the session expires or if the json file is moved.

Contributions
=================
Source contributions, suggestions and pull requests are very welcome.

If you are experiencing playback issues, please report this to the Mopidy-Tidal issue tracker and/or check Python-Tidal for relevant issues.

Project resources
=================

- `Source code <https://github.com/tehkillerbee/mopidy-tidal>`_
- `Issue tracker <https://github.com/tehkillerbee/mopidy-tidal/issues>`_
- `Python-Tidal repository <https://github.com/tamland/python-tidal>`_
- `Python-Tidal issue tracker <https://github.com/tamland/python-tidal/issues>`_


Credits
=======

- Original author: `mones88 <https://github.com/mones88>`__
- Current maintainer: `tehkillerbee <https://github.com/tehkillerbee>`__
- `Contributors <https://github.com/tehkillerbee/mopidy-tidal/graphs/contributors>`_


Changelog
=========

v0.2.7
----------------------------------------
- Use path extension for Tidal OAuth cache file
- Improved error handling for missing images, unplayable albums
- Improved playlist browsing

v0.2.6
----------------------------------------
- Improved reliability of OAuth cache file generation.
- Added optional client_id & client_secret to [tidal] in mopidy config (thanks Glog78)
- Removed username/pass, as it is not needed by OAuth (thanks tbjep)

v0.2.5
----------------------------------------
- Reload existing OAuth session on Mopidy restart
- Added OAuth login support from tidalapi (thanks to greggilbert)

v0.2.4
----------------------------------------
- Added track caching (thanks to MrSurly and kingosticks)

v0.2.3
----------------------------------------
- fixed python 3 compatibility issues
- Change dependency tidalapi4mopidy back to tidalapi (thanks to stevedenman)

v0.2.2
----------------------------------------
- added support browsing of favourite tracks, moods, genres and playlists (thanks to SERVCUBED)


v0.2.1
----------------------------------------
- implemented get_images method
- updated tidal's api key


v0.2.0
----------------------------------------
- playlist support (read-only)
- implemented artists lookup
- high and low quality streams should now work correctly
- cache search results (to be improved in next releases)

v0.1.0
----------------------------------------

- Initial release.
