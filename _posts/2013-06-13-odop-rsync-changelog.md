---
layout: post
title: "ODOP rsync changelog"
description: ""
category: 
tags: [ODOP]
---
{% include JB/setup %}

From : [http://linux.softpedia.com/progChangelog/rsync-Changelog-192.html](http://linux.softpedia.com/progChangelog/rsync-Changelog-192.html)

what's new in rsync 3.0.9 Pre1:  
June 28th, 2011

- Fix a crash bug in checksum scanning when --inplace is used.
- Fix preservation of a symlink's system xattrs (e.g. selinux) on Linux.
- Fix a bug with the modifying of unwritable directories.
- Fix --fake-super's interaction with --link-dest same-file comparisons.
- Fix the updating of the curr_dir buffer to avoid a duplicate slash.
- Make daemon-exclude file errors more error-like.
- Fix some issue with the post-processing of the man pages.

What's new in rsync 3.0.8 Pre1:  
February 23rd, 2011

Bug FIXES:

- Fixed two buffer-overflow issues: one where a directory path that is exactly MAXPATHLEN was not handled correctly, and one handling a --backup-dir that is extra extra large.
- Fixed a data-corruption issue when preserving hard-links without preserving file ownership, and doing deletion either before or during the transfer. This fixes some assert errors int the hard-linking code, and some potential failed checksums (via -c) that should have matched.
- Fixed a potential crash when an rsync daemon has a filter/exclude list and the transfer is suing ACLs or xattrs.
- Fixed a hang if a really large file is being processed by an rsync that can't handle 64-bit numbers. Rsync will now complain about the file being too big and skip it.
- For devices and special files, we now avoid gathering useless ACL and/or xattr information for files that aren't copied. (The un-copied files are still put into the file list, but there's no need to gather data that is not going to be used.) This ensures that if the user uses --no-D, that rsync can't possibly complain about being unable to gather extended information from special files that are in the file list (but not in the transfer).
- Properly handle requesting remote filenames that start with a dash. This avoids a potential error where a filename could be interpreted as a (usually invalid) option.
- Fixed a bug in the comparing of upper-case letters in file suffixes for --skip-compress.
- If an rsync daemon has a module configured without a path setting, rsync will now disallow access to that module.
- If the destination arg is an empty string, it will treated as a reference to the current directory (as 2.x used to do).
- If rsync was compiled with a newer time-setting function (such as lutimes), rsync will fall-back to an older function (such as utimes) on a system where the newer function is not around. This helps to make the rsync binary more portable in mixed-OS-release situations.
- Fixed a batch-file writing bug that would not write out the full set of compatibility flags that the transfer was using. This fixes a potential protocol problem for a batch file that contains a sender-side I/O error; i would have been sent in a way that the batch-reader wasn't expecting.
- Some improvements to the hard-linking code to ensure that device-number hashing is working right, and to supply more information if the hard-link code fails.
- The --inplace code was improved to not search for  and impossible checksum position. The quadruple-verbose chunk\[N\] message will now mention when an inplace chunk was handled by a seek rather than a read+write.
- If we fail to connect to an rsync daemon, report all the connection errors (e.g. IPv4 & IPv6), not just the last one.
- Improved ACL mask handling, e.g. for Solaris.
- Fixed an issue where an xattr and/or ACL transfer that used an alt-dest option (e.g. --link-dest) could output an error trying to itemize the changes against the alt-dest directory's xattr/ACL info but was instead trying to access the not-yet-existing new destination directory.
- Improved xattr system-error message to mention the full path to the file.
- The --link-dest checking for identical symlinks now avoids considering attribute differences that cannot be changed on the receiver.
- Avoid trying to read/write xattrs on certain file types for certain OSes. Improved configure to set NO_SYMLINK_XATTRS, NO_DEVICE_XATTRS, and/or NO_SPECIAL_XATTRS defines in config.h
- Improved the unsafe-symlink errors messages.
- Fixed a bug setting xattrs on new files that aren't user writable.
- Fixed a bug with --fake-super when copying files and dirs that aren't user writable.
- Fixed a bug where a sparse file could have its last sparse block turned into a real block when rsync sets the file size (requires ftruncate).
- If a temp-file name is too long, rsync now avoids truncating the name in the middle of adjacent high-bit characters. This prevents a potential filename error if the filesystem doesn't allow a name to contain an invalid multi-byte sequence.
- If a muli-protocol socket connection fails (i.e., when contacting a daemon), we now report all the failures, not just the last one. This avoids losing a relevant error (e.g. an IPv4 connection-refused error) that happened before the final error (e.g. an IPv6 protocol-not-supported error).
- Generate a transfer error if we try to call chown with a -1 for a uid or a gid (which is not settable).
- Fixed a forceful delete of a file with --one-file-system.
- Fix the popt arg parsing so that an option that doesn't take  an arg will reject an attempt to supply one.
- A couple minor option tweaks to support/rrsync script, and also some regex changes that make vim hightlighting happier.
- Fixed some issues in the support/mnt-excl script.
- A few manpage improvements.

ENHANCEMENTS:

- Added ".hg/" to the default cvs excludes (see -C & --cvs-exclude).

DEVELOPER RELATED:

- Use lchmod() whenever it is available (not just on symlinks).
- A couple fixes to the socketpair_tcp() routine.
- Updated the helper scripts in the packaging subdirectory.
- Renamed configure.in to configure.ac.


what's new in rsync 3.0.6:  
May 9th, 2009

- Fixed a --read-batch hang when rsync is reading a batch file that was created from an incremental-recursion transfer.
- Fixed the daemon's socket code to handle the simultaneous arrival of multiple connections.
- Fix --safe-links/--copy-unsafe-links to properly handle symlinks that have consecutive slashes in the value.
- Fixed the parsing of an IPv6_LITERAL_ADDR when a USER@ is prefixed.
- The sender now skips a (bogus) symlink that has a 0-length value, which avoids a transfer error in the receiver.
- Fixed a case where the sender could die with a tag-0 error if there was an I/O during the sending of the file list.
- Fixed the rrsync script to avoid a server-side problem when -e is at the start fo the short options.
- Fixed a problem where a vanished directory could turn into an exit code 23 instead of the proper exit code 24.
- Fixed the --iconv conversion of symlinks when doing a local copy.
- FIxed a problem where --one-file-system was not stopping deletion on the receiving side when a mount-point directory did not match a directory in the transfer.
- Fixed the dropping of an ACL mask when no named ACL values were present.
- Fixed an ACL/xattr corruption issue where the --backup option could cause rsync to associate the wrong ACL/xattr information with recived files.
- Fixed the use of --xattrs with --only-write-batch.
- Fixed the use of --dry-run with --read-batch.
- Fixed configure's erroneous use of target.
- Fixed configure's --disable-debug option.
- Fixed a run-time issue for systems that can't find iconv_open() by adding the --disable-iconv-open configure option.
- Complain and die if the user tries to combine --remove-source-files (or the deprecated --remove-sent-files) with --read-batch
- Fixed an failure transferring special files from SOlaris to Linux.

