# Disks and File Systems

#### Archiving vs Compressing

- Archiving packs multiple files and directories into a single file: `tar -cf files file1 file2` gives me `files.tar`
- Compressing is reducing the size: `gzip file1` gives me `file1.gz`. `gzip` is for zipping, and `gunzip` is for unzipping. It is not *gun-zip*, it is *g-unzip*. It all makes a lot of sense now. 🤦
- These generally go hand in hand, which is how we end up with `.tar.gz` files or `.tgz`.
- If you want to view the contents of a file before extracting them, `tar -tvf <filename>.tar`.
- To decompress and unarchive a file we do: `tar -xvfz <filename>.tar.gz`, where `z` is for `zcat` which is pretty much`gunzip` with a couple flags.


#### Linux directory hierarchy

Here's a [blogpost from linuxhandbook](https://linuxhandbook.com/linux-directory-structure/) explaining it. Highlights:
- `/etc` is pronounced EHT-see, like the store and not et cetera. 🤦
- `/tmp` is temporary files that get wiped, but `/var/tmp` isn't.
- `/opt` is for additional third-party software. Not widely used, but the general practice is to symlink the binary from `/opt` to `/bin`.
- `/usr/local/include` has the header files used by the C compiler.

