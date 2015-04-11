# Introduction #

If you're here, chances are you know what MogileFS is.  If not, it's a distributed storage mechanism similar to Amazon's S3, except you own and control the hardware.  It runs on linux, uses standard databases (typically MySQL) and any underlying filesystem you wish.


## Installation ##
  * Prerequisites
  * Installation
    * [From CPAN](InstallFromCPAN.md)
    * [From Subversion](InstallFromSubversion.md) (latest and greatest)
  * [Setting up your trackers](TrackerSetup.md)

## Storing Files in MogileFS ##
  * [Overview](StorageOverview.md)
  * [Setup ](StorageSetup.md): Brief guide to setting up your storage nodes
  * [Using lighttpd or apache instead of mogstored](MogstoredAlternatives.md)

## Serving Files from MogileFS ##
  * [Serving File from MogileFS](ServingOverview.md)
  * [Optimizing your MogileFS Cluster](OptimizationNotes.md)