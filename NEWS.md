Changes in dtrx
===============

Version 7.1
-----------

New features
~~~~~~~~~~~~

 * LZH archives are now supported.

Bug fixes
~~~~~~~~~

 * dtrx will no longer offer to extract the zero archive files found in a
   zero-file archive.

 * Temporary directories will be cleaned up after extracting an empty
   archive.

Version 7.0
-----------

At this point, I consider dtrx to be mature software.  It's maybe a little
too interactive, but otherwise it does everything I want, and it does it
very well.  Expect new releases to be few and far between going forward.

New features
~~~~~~~~~~~~

 * If any of dtrx's command line arguments are URLs, it will automatically
   download them with `wget -c` in the current directory before extracting
   them.  See the documentation for more information about this feature.
   Note that there might be trouble if there's already a file in the
   directory where wget would normally save the download.

Enhancements
~~~~~~~~~~~~

 * dtrx will try to extract ZIP files with 7z if unzip is not successful.
   Thanks to Edward H for reporting this bug.

 * dtrx will be smarter about removing extensions from filenames when
   extracting to a new directory or file.

 * dtrx will not ask you if you want to recurse through an archive if
   the number of archives inside the original file is small.

Version 6.6
-----------

Enhancements
~~~~~~~~~~~~

 * dtrx can now handle `xz compression`_.

.. _xz compression: http://tukaani.org/xz/

Other changes
~~~~~~~~~~~~~

 * The tests now use the PyYAML library, instead of the abandoned Syck.
   Thanks to Miguelangel Jose Freitas Loreto for a patch.

Version 6.5
-----------

Enhancements
~~~~~~~~~~~~

 * When you list archive contents with -l or -t, dtrx will start printing
   results much faster than it used to.  There's a small chance that it
   will print some incorrect listings if it misdetects the archive type of
   a given file, but it will show you an error message when that happens.

 * dtrx recognizes more kinds of compressed tar archives by their
   extension.

 * You can now extract newer .deb packages that are compressed with bzip2
   or lzma.

Bug fixes
~~~~~~~~~

 * When extracting an archive that contained a file with a mismatched
   filename, the prompt would offer you a chance to "rename the directory"
   instead of "rename the file."  This wording has been fixed, along with
   some other wording adjustments in the prompts generally.

 * Perform more reliable detection of the terminal size, and improve word
   wrapping on prompts.

Other changes
~~~~~~~~~~~~~

 * The README is now written like a man page, and can be converted to a man
   page by using rst2man_.

.. _rst2man: http://docutils.sourceforge.net/sandbox/manpage-writer/

Version 6.4
-----------

Enhancements
~~~~~~~~~~~~

 * Support detection of LZMA archives by magic.

 * Interactive prompts are wrapped much more cleanly.

Bug fixes
~~~~~~~~~

 * Fix a bug where dtrx would crash when extracting an archive with no
   files inside it.

Version 6.3
-----------

New features
~~~~~~~~~~~~

 * Add support for RAR archives.  Thanks to Peter Kelemen for the patch.

Bug fixes
~~~~~~~~~

 * Previous versions of dtrx would fail to extract certain archive types
   with the ``-v`` option specified.  This has been fixed.

 * dtrx 6.3 no longer imports the sets module unless it's running under a
   very old version of Python, to avoid deprecation warnings under Python
   2.6.

Version 6.2
-----------

New features
~~~~~~~~~~~~

 * --one-entry option: Normally, if an archive only contains one file or
   directory with a name that doesn't match the archive's, dtrx will ask
   you how to handle it.  With this option, you can specify ahead of time
   what should happen.

Bug fixes
~~~~~~~~~

 * Since version 6.0, when you extracted or listed the contents of a cpio
   archive, dtrx would display a warning that simply said "1234 blocks."
   dtrx 6.2 suppresses this message.

 * When you try to list the contents of an archive, dtrx will now cope with
   misnamed files more gracefully, giving more accurate results and showing
   fewer error messages.

 * dtrx 6.2 will only show you error messages from archive extraction if it
   is completely unable to extract the file.  If one of its extraction
   methods succeeds, it will no longer show you the error messages from
   previous extraction attempts.

 * dtrx is now better about cleaning up partially extracted archives when
   it encounters an error or signal.

 * Users will no longer see error messages about broken pipes from dtrx.

Version 6.1
-----------

New features
~~~~~~~~~~~~

 * Add support for InstallShield archives, using the unshield command.

 * The wording of many of the interactive prompts has been adjusted,
   hopefully to be clearer and provide more information to the user
   immediately.

Bug fixes
~~~~~~~~~

 * dtrx 6.1 does a better job protecting against race conditions when
   extracting a single file.

 * If you used the -f option, and extracted an archive that only contained
   one file or directory, dtrx 6.0 would still prompt you to ask how it
   should be extracted.  dtrx 6.1 fixes this, extracting the contents to
   the current directory as -f requires.

 * Recursive extraction would not work well in dtrx 6.0 when the contents
   of the original archive were a single file.  This has been fixed in dtrx
   6.1.

Version 6.0
-----------

New features
~~~~~~~~~~~~

 * When you specify -v at the command line, dtrx will display the files it
   extracts, much like tar.

 * When dtrx prompts you about how to handle recursive archives, you now
   have the option of listing what those archives before making a decision.

 * dtrx will now provide more information about why a particular extraction
   attempt failed.  It will show you error messages from all the attempts
   it made, rather than only the last error it got.  It will also detect
   and warn you when one of the underlying extraction tools, like
   cabextract, cannot be found.

 * dtrx does a better job of cleaning up after itself.  It wouldn't always
   clean up temporary files after certain errors; that has been fixed.  It
   also catches SIGINT and SIGTERM and cleans up before finishing
   execution.

Bug fixes
~~~~~~~~~

 * Version 5.0 introduced a regression such that dtrx would not offer to
   extract recursive archives that were hidden under subdirectories.
   Version 6.0 fixes that.

 * dtrx would not properly extract recursive archives when the original
   archive contained a single directory.  This has been fixed.

Version 5.1
-----------

Bug fixes
~~~~~~~~~

 * Version 5.0 did not work with Python 2.3; it used a new language
   feature.  This release fixes that.

Version 5.0
-----------

New features
~~~~~~~~~~~~

 * dtrx can now extract Ruby gems, 7z archives, and Microsoft Cabinet
   archives.  It can also handle files compressed with lzma, and extract
   the metadata from Debian packages and Ruby gems.

 * dtrx will now use several strategies to try to figure out what kind of
   file you have, and extract it accordingly.  If one doesn't work, it'll
   try something else if it can.

 * dtrx now displays more helpful errors when things go wrong.

 * Previous versions of dtrx would look at what files were included in an
   archive, and then make a decision about how to extract it.  Now, it
   always extracts files to a temporary directory, and figures out what to
   do with that directory afterward.  This should be slightly faster and
   nicer to the system.

Version 4.0
-----------

New features
~~~~~~~~~~~~

 * dtrx is now interactive.  If the archive only contains one item, or
   contains other archives, dtrx will ask you how you would like to handle
   it.  You can turn these questions off the the -n option.

 * There is a new -l option, which simply lists the archive's contents
   rather than extracting them.
