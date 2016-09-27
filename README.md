## Introduction

This script extracts messages from a Hypermail mailing list archive in XHTML format and outputs them as a Unix mbox file.  This might be useful if, say, you're converting from [Hypermail](http://www.hypermail-project.org/) 2.1.8+ to [MHonArc](http://www.mhonarc.org/).

*hm2mbox* is written in Perl.  It should work on any system with Perl 5.005 or better.  It also requires the following Perl modules:

* `Carp`
* `File::Basename`
* `File::Find`
* `Getopt::Long`
* `HTML::Entities`
* `MIME::Lite`
* `Text::Balanced`

If your system does not have these modules installed already, visit [CPAN](http://search.cpan.org/).  Note that `HTML::Entities` and `MIME::Lite` are not included with the default Perl distribution so you may need to install them yourself.  Also note that `Text::Balanced` does not work with
versions of Perl older than 5.005; further, it is not included with Perl distributions prior to 5.8.0 so you will probably need to install it if you're running an older version of Perl.


## Installation

* Retrieve [the script](hm2mbox) and save it locally.
* Verify ownership and permissions on the script.
* Edit the script and adjust the location of the perl interpreter in the first line if necessary.


## Use

To use *hm2mbox*, pass it the name of the directory holding the Hypermail archives.  The script will recurse the directory, extract the contents of each message, and write the results to standard output.  If a message has associated attachments, it will include those as well.  If you'd like to see copious debugging messages while the script runs, specify the `-d` option.

Examples:

| Invocation | Meaning |
| ---------- | ------- |
| `hm2mbox listdir > mbox` | converts messages in hypermail archive 'listdir' to a Unix mbox file. |
| `hm2mbox -d listdir > mbox` | same as above but with copious debugging messages. |


## Known Bugs and Caveats

Currently, I am not aware of any bugs in this script.  At the same time, though, I am not certain how robust it is since I have not tested it on a variety of Hypermail archives.

This script requires that messages be formatted as XHTML.  If you're trying to convert an archive from a version of Hypermail before 2.1.8, when XHTML support was introduced, look at [Anthony W's h2mbx.pl script](http://www.aspidastra.com/anthonyw/mhonarc/h2mbx.pl-script.txt).

Understand that it is not possible to regenerate messages perfectly from the hypermail archives and that, as a result, things like GnuPG signatures are unlikely to be valid.

If you encounter an error similar to `Insecure dependency in chdir while running with -T switch at /usr/lib/perl/5.00503/File/Find.pm line 133` when trying to run *hm2mbox*, it's likely that you're using an older version of the Perl module `File::Find`.  Versions distributed with Perl versions prior to 5.6.0 don't support the `no_chdir` option, which is used in this script to avoid problems with taint checks.  The solution is to
either upgrade `File::Find`, upgrade Perl itself, or disable taint checks (ie, remove the `-T` option on the first line of the script).

If you encounter a problem using this script, I encourage you to enable debug mode (eg, add `-d` to your commandline) and examine the output it produces before contacting me.  Often, this will enable you to resolve the problem yourself.


## Copyright and License

Copyright (c) 2004-2016, George A. Theall.
All rights reserved.

This script is free software; you can redistribute it and/or modify it under the same terms as Perl itself.
