# Overview 

This program selects and prints the read id of the first read in a BAM file. 

The input is a single BAM file and the output is a single string indicating the read id. 

In the examples below, `$` indicates the command line prompt.

# Licence

This program is released as open source software under the terms of [MIT License](https://raw.githubusercontent.com/bjpop/bamreadid/main/LICENSE).

# Installing

This is a BASH shell script. Copy it to your local computer to install. It can be run from any directory.

## Dependencies

This program depends on:
 * samtools
 * awk
 * BASH

It will fail with an error message if these dependenies are not available in the PATH on your computer.

You will need to install these dependencies yourself if they aren't already available on your local system.

# Usage 

## Help message

`bamreadid` can display usage information on the command line via the `-h`:

```
$ ./bamreadid -h 
bamreadid: Get the read identifer from the first read in a BAM file. 
Usage:
    bamreadid [-h] -i input_bam_file_name 

   -i <input_bam_file_name> is required, this specifies the input BAM file name

   -h                       displays an help message
                     
Example:
    bamreadid -i example.bam 
Dependencies:
   The following tools must be installed on your computer to use this script,
   and be accessible via the PATH environment variable:
   - bash 
   - samtools 
   - awk
```

## General usage 

The simplest use case is to specify a BAM file on the command line with the `-i` parameter:
```
./bamreadid -i /path/to/bam/file
```
where `/path/to/bam/file` is the filepath to your input BAM file.

If you have many samples to process then the following BASH loop might be useful, assuming ``bamreadid`` is in your PATH (otherwise specify the path to the script):

```
for file in *.bam; do
    sample=$(basename $file .bam)
    readid=$(bamreadid -i $file)
    echo "$sample,$readid"
done
```

## Exit status values

`bamreadid` returns the following exit status values:

* 0: The program completed successfully.
* 1: File I/O error. This can occur if the input BAM file cannot be opened for reading. This can occur because the file does not exist at the specified path, or `bamreadid` does not have permission to read from the file. 
* 2: A command line error occurred. This can happen if the user specifies an incorrect command line argument. In this circumstance bamreadid will also print a usage message to the standard error device (stderr).

# Bug reporting and feature requests

Please submit bug reports and feature requests to the issue tracker on GitHub:

[bamreadid issue tracker](https://github.com/bjpop/bamreadid/issues)
