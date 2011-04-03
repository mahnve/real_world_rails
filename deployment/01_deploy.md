!SLIDE 

# Passenger

* mod_ruby
* Apache
* nginx

!SLIDE commandline

    $ gem install passenger 

    Building native extensions.  This could take a while...
    Successfully installed fastthread-1.0.7
    Successfully installed daemon_controller-0.2.6
    Successfully installed spruz-0.2.5
    Successfully installed file-tail-1.0.5
    Successfully installed passenger-3.0.5
    5 gems installed

!SLIDE commandline

    $  passenger-install-apache2-module

    This installer will guide you through the entire installation process. It
    shouldn't take more than 3 minutes in total.

    Here's what you can expect from the installation process:

    1. The Apache 2 module will be installed for you.
    2. You'll learn how to configure Apache.
    3. You'll learn how to deploy a Ruby on Rails application.

    Don't worry if anything goes wrong. This installer will advise you on how to
    solve any problems.

    Press Enter to continue, or Ctrl-C to abort

!SLIDE

# [Unicorn](https://github.com/defunkt/unicorn)

* For those times when Passenger is not an option
* Runs as separate processes, proxied from web server

!SLIDE

# SysLogLogger

* Logs to system logger
* Configuration in syslog-ng, rsyslog ...
