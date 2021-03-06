# journald-native

[![Gem Version](https://badge.fury.io/rb/journald-native.svg)](http://badge.fury.io/rb/journald-native)
[![Reference Status](https://www.versioneye.com/ruby/journald-native/reference_badge.svg)](https://www.versioneye.com/ruby/journald-native/references)

A systemd-journal native logging lib wrapper.
[See sd-journal help for more info](http://www.freedesktop.org/software/systemd/man/sd_journal_print.html)

## Usage

```ruby
require 'journald/native'
```

### Constants

Constants are used to denote a log level

Available constants:

```ruby
Journald::LOG_EMERG     # system is unusable
Journald::LOG_ALERT     # action must be taken immediately
Journald::LOG_CRIT      # critical conditions
Journald::LOG_ERR       # error conditions
Journald::LOG_WARNING   # warning conditions
Journald::LOG_NOTICE    # normal but significant condition
Journald::LOG_INFO      # informational
Journald::LOG_DEBUG     # debug-level messages
```

systemd-journal uses syslog constants to denote level therefore they are equal to those of the Syslog module,
e.g. ```Journald::LOG_WARNING == Syslog::LOG_WARNING```.
[See syslog man page for more info](http://man7.org/linux/man-pages/man3/syslog.3.html)

### Methods

Methods of Journald::Native class wrap systemd-journal calls.
[See sd-journal help for more info](http://www.freedesktop.org/software/systemd/man/sd_journal_print.html)

```ruby
Journald::Native.send "MESSAGE=message", "PRIORITY=#{Journald::LOG_WARNING}"
Journald::Native.print Journald::LOG_WARNING, "message"
Journald::Native.perror "message"
```

It is not recommended to use ```print``` and ```perror``` as you may get exception if your string contains
```'\0'``` byte due to C zero-terminated string format. On the contrary ```send``` uses binary buffers and
does not have this shortcoming.

### License

The gem is available as open source under the terms of the GNU Lesser General Public License, version 2.1
or later.
