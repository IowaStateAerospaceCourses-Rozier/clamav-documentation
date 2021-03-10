# Signature Testing and Management

Table Of Contents

<!-- TOC depthFrom:2 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Signature Testing and Management](#signature-testing-and-management)
  - [Freshclam](#freshclam)
  - [Sigtool](#sigtool)
  - [ClamBC](#clambc)
  - [Next Steps](#next-steps)
  - [Create your own signatures](#create-your-own-signatures)

<!-- /TOC -->

_Tip_: The commands on Windows are generally the same, but you may need to add the `.exe` extension to run the ClamAV applications.

## Freshclam

Before you can start the ClamAV scanning engine (using either `clamd` or `clamscan`), you must _first_ have ClamAV Virus Database (.cvd) file(s) installed in the appropriate location on your system.

The tool `freshclam` is used to download and update ClamAV’s official virus signature databases. While easy to use in its base configuration, `freshclam` does require a working [`freshclam.conf` configuration file](Usage/Configuration.md#freshclamconf) to run (the location of which can be passed in via command line if the default search location does not fit your needs).

Once you have a valid configuration file, you can invoke Freshclam with the following command:

> `$ freshclam`

By default, `freshclam` will then attempt to connect to ClamAV's virus signature database distribution network. If no databases exist in the directory specified, `freshclam` will do a fresh download of the requested databases. Otherwise, `freshclam` will attempt to update existing databases, pairing them against downloaded cdiffs. If a database is found to be corrupted, it is not updated and instead replaced with a fresh download.

Of course, all this behaviour--and more--can be changed to suit your needs by [modifying `freshclam.conf` and/or using various command line options](Usage/Configuration.md#freshclamconf).

You can find more information about Freshclam with the commands:

Unix/Linux:

> `$ freshclam --help`

Or (Unix/Linux only):

> $ `man freshclam`

_Tip_: Newer versions of Freshclam will create your database directory if it doesn't already exist. Older versions won't, and may fail unless you create it first.

## Sigtool

ClamAV provides `sigtool` as a command-line testing tool for assisting users in their efforts creating and working with virus signatures. While sigtool has many uses--including crafting signatures--of particular note, is sigtool's ability to help users and analysts in determining if a file detected by *libclamav*'s virus signatures is a false positive.

This can be accomplished by using the command:

> $ `sigtool --unpack=FILE`

Where FILE points to your virus signature databases. Then, once `sigtool` has finished unpacking the database into the directory from which you ran the command, you can search for the offending signature name (provided either by [`clamscan`](Scanning.md#clamscan) scan reports or [`clamd`](Scanning.md#clamd) logs). As an example:

> $ `grep "Win.Test.EICAR" ./*`

Or, do all that in one step with:

> $ `sigtool --find="Win.Test.EICAR"`

This should give you the offending signature(s) in question, which can then be included as part of your [false positive report](https://www.clamav.net/reports/fp).

To learn more in depth information on how `sigtool` can be used to help create virus signatures and work with malicious (and non-malicious) files please reference the many online tutorials on the topic.

Otherwise, information on available sigtool functions can be easily referenced with:

> $ `sigtool --help`

Or (Unix/Linux only):

> $ `man sigtool`

## ClamBC

`clambc` is Clam Anti-Virus’ bytecode signature testing tool. It can be used to test newly crafted bytecode signatures or to help verify existing bytecode is executing against a sample as expected.

For more detailed help, please use:

> $ `clambc --help`

Or (Unix/Linux only):

> $ `man clambc`

## Next Steps

Now that you know more about Freshclam and tools to work with the signature databases, it's time to [run your first scan](Scanning.md).

## Create your own signatures

There is a whole community of malware researchers and signature writers. If you'd like to learn how to [craft your own signatures](../Signatures.md), you can!