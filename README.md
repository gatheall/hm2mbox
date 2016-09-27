<HTML>
<HEAD>
<TITLE>hm2mbox</TITLE>
<LINK REV="made" HREF="mailto:theall@tifaware.com">
<LINK REL="shortcut icon" HREF="http://www.tifaware.com/favicon.ico">
</HEAD>

<!--#include virtual="/header.html"-->
<!--#if expr="$weblint" -->
<BODY BGCOLOR="#FFFFFF">
<!--#endif -->


<H4 ALIGN="center">
   <A HREF="/">TifaWARE</A> |
   <A HREF="../">Perl Programs</A> |
   hm2mbox
</H4>
                                                                                
                                                                                
<HR>
<H2>hm2mbox</H2>

<H3>Introduction</H3>

<P>This script extracts messages from a Hypermail mailing list archive
in XHTML format and outputs them as a Unix mbox file.  This might be
useful if, say, you're converting from <A
HREF="http://www.hypermail.org/">Hypermail</A> 2.1.8+ to <A
HREF="http://www.mhonarc.org/">MHonArc</A>.</P>

<P><B>hm2mbox</B> is written in Perl.  It should work on any system with
Perl 5.005 or better.  It also requires the following Perl modules:</P>

<UL>
   <LI><CODE>Carp</CODE></LI>
   <LI><CODE>File::Basename</CODE></LI>
   <LI><CODE>File::Find</CODE></LI>
   <LI><CODE>Getopt::Long</CODE></LI>
   <LI><CODE>HTML::Entities</CODE></LI>
   <LI><CODE>MIME::Lite</CODE></LI>
   <LI><CODE>Text::Balanced</CODE></LI>
</UL>

<P>If your system does not have these modules installed already, visit
<A HREF="http://search.cpan.org/">CPAN</A>.  Note that
<CODE>HTML::Entities</CODE> and <CODE>MIME::Lite</CODE> are not included
with the default Perl distribution so you may need to install them
yourself.  Also note that <CODE>Text::Balanced</CODE> does not work with
versions of Perl older than 5.005; further, it is not included with Perl
distributions prior to 5.8.0 so you will probably need to install it if
you're running an older version of Perl.</P>


<H3>Installation</H3>

<OL>
   <LI>Retrieve the script <A HREF="/code/hm2mbox/hm2mbox">hm2mbox</A>
      and save it locally.  You may also wish to verify its
      <A HREF="/code/hm2mbox/hm2mbox.md5">MD5 checksum</A> or, better, its
      <A HREF="/code/hm2mbox/hm2mbox.asc">GPG signature</A> against
      <A HREF="/~theall/gpg.html">my current GPG key</A>.</LI>
   <LI>Verify ownership and permissions on the script.</LI>
   <LI>Edit the script and adjust the location of the perl 
      interpreter in the first line if necessary.</LI>
</OL>


<H3>Use</H3>

<P>To use <B>hm2mbox</B>, pass it the name of the directory holding the
Hypermail archives.  The script will recurse the directory, extract the
contents of each message, and write the results to standard output.  If
a message has associated attachments, it will include those as well.  If
you'd like to see copious debugging messages while the script runs,
specify the <CODE>-d</CODE> option.</P>

<P>Examples:</P>
<BLOCKQUOTE>
<DL>
   <DT><CODE>hm2mbox listdir &lt; mbox</CODE></DT>
   <DD>converts messages in hypermail archive 'listdir' to a Unix mbox file.</DD>

   <DT><CODE>hm2mbox -d listdir &lt; mbox</CODE></DT>
   <DD>same as above but with copious debugging messages.</DD>
</DL>
</BLOCKQUOTE>


<H3>Known Bugs and Caveats</H3>

<P>Currently, I am not aware of any bugs in this script.  At the same
time, though, I am not certain how robust it is since I have not tested
it on a variety of Hypermail archives.</P>

<P>This script requires that messages be formatted as XHTML.  If you're
trying to convert an archive from a version of Hypermail before 2.1.8,
when XHTML support was introduced, look at <A
HREF="http://www.albany.net/~anthonyw/mhonarc/h2mbx.pl-script.txt">
Anthony W's h2mbx.pl script</A>.</P>

<P>Understand that it is not possible to regenerate messages perfectly
from the hypermail archives and that, as a result, things like GnuPG
signatures are unlikely to be valid.</P>

<P>If you encounter an error similar to <CODE>Insecure dependency in
chdir while running with -T switch at /usr/lib/perl/5.00503/File/Find.pm
line 133</CODE> when trying to run <B>hm2mbox</B>, it's likely that
you're using an older version of the Perl module
<CODE>File::Find</CODE>.  Versions distributed with Perl versions prior
to 5.6.0 don't support the <CODE>no_chdir</CODE> option, which is used
in this script to avoid problems with taint checks.  The solution is to
either upgrade <CODE>File::Find</CODE>, upgrade Perl itself, or disable
taint checks (ie, remove the <CODE>-T</CODE> option on the first line of
the script).</P>

<P>If you encounter a problem using this script, I encourage you to
enable debug mode (eg, add <CODE>-d</CODE> to your commandline) and
examine the output it produces before contacting me.  Often, this will
enable you to resolve the problem yourself.</P>


<H3>Copyright and License</H3>

<P>Copyright (c) 2004, George A. Theall.<BR>
All rights reserved.</P>

<P>This script is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.</P>


<H3>History</H3>

<CENTER>
<TABLE CELLPADDING="5" CELLSPACING="0" WIDTH="95%" BORDER="1">
   <TR>
      <TH ALIGN="left">Date </TH>
      <TH ALIGN="left">Version </TH>
      <TH ALIGN="left">Verification </TH>
      <TH ALIGN="left">Notes<BR></TH>
   </TR>
   <TR>
      <TH ALIGN="left" VALIGN="top">06-Jul-2004 </TH>
      <TD ALIGN="left" VALIGN="top"><A HREF="/code/hm2mbox/hm2mbox-1.00">1.00</A> </TD>
      <TD ALIGN="left" VALIGN="top"><A HREF="/code/hm2mbox/hm2mbox-1.00.md5">MD5</A> / 
         <A HREF="/code/hm2mbox/hm2mbox-1.00.asc">GPG</A> </TD>
      <TD ALIGN="left" VALIGN="top">
      <UL>
         <LI>Initial version.</LI>
      </UL></TD>
   </TR>
</TABLE>
</CENTER>


<HR>
<H4 ALIGN="center">
   <A HREF="/">TifaWARE</A> |
   <A HREF="../">Perl Programs</A> |
   hm2mbox
</H4>
                                                                                

<!-- $Id$ -->
                                                                                
<!--#include virtual="/footer.html" -->
<!--#if expr="$weblint" -->
</BODY>
<!--#endif -->
</HTML>
