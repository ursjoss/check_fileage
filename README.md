# check_fileage

## Purpose

Nagios plugin to check if a file is present or not and if it has changed within a certain time.

## Origination of the script

Adapting check_fileage.py (by Craig Rayner - many thanks!) to my needs. Source https://exchange.nagios.org/directory/Plugins/System-Metrics/File-System/File-Age-Check/details

Description from exchange.nagios.org:

    This Python script works on both Windows and *nix boxes and returns the date of
    the file (modified, access, or create) in human understandable form. (Only English.)
    Will check Windows \serversharepathfile type addresses, but you may need to alter
    the NRPE Service privilege to do so. 
    Return the basename of the file with the time date information as well as the type
    of time it checked. 

    Usage: check_fileage.py -f /mount/path/file.ext -w nnnn -c nnnn C|M -V -h 

    Tested on Window W2K3 and XP, and Centos 4.4 using Python 2.5

## Additional requirements

The original script requires the file to be present. If it is missing, the script returns 'unknown'.

I had a slightly different use case. I needed to verify that a particular file is either

- not present
- or if present it is younger than the specified time

If it is present and older than the specified time, a warn or critical state is returned.

I therefore added two additional parameters:

         -x, --fail-on-not-exists
            Returns WARN if the file does not exist.
         -X, --ok-on-not-exists
            Returns OK if the file does not exist.
            
If none of those parameters is supplied, the file shows the original behavior of returning 'unknown'.

