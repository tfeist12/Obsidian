rarely seeing timeout before expected number of messages sent

check if timeout occurs
only begin timeout timer after first status sent
don't use waitgroups for timing based issues
set up timing tests to not be dependent on system time