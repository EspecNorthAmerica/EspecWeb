# EspecWeb
Issue Tracker &amp; documentation for Espec Universal Web Controller.

Updates currently must be distrubuted via the [espec service department](http://www.espec.com/na/support/).

Current Version: 2.1.2

2.1.2:
  * Bug fixes for multi controller chambers.
2.1.1:
  * Add better descriptions of chamber config options.
  * Add icons for loop names (defaults to none)
2.1.0:
  * Merge multiple page system into a single page approach.
  * Add support for for cascade on the WatlowF4T
  * Add support for the Espec P300 chamber controller.
  * Add support for the Espec SCP-220 chamber controller.
  * Add TCP direct interface to chamber controller.
    * Port 502 for modbus based chamber controllrs (WatlowF4T)
    * Port 10001 for Espec P300/SCP-220
  * Add REST API.
  * Add message when server is offline.
  * Add new first configuration wizard.
  * Notify user of non working browsers (ie8 and older)
  * Switch to MySQL backend, (this makes updating from 2.0.0 difficult.
  * Move background error messages to setup screen to stop spamming user with non critical errors.
  * Add support for multi-controller chambers ie large IR chambers.
2.0.0:
  * Initial Release, WatlowF4T support only.
