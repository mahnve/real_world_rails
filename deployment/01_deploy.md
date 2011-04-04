!SLIDE subsection

# Deployment

!SLIDE bullets

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

!SLIDE bullets

# [Unicorn](https://github.com/defunkt/unicorn)

* For those times when Passenger is not an option
* Runs as separate processes, proxied from web server

!SLIDE bullets

# SysLogLogger

* Logs to system logger
* Configuration in syslog-ng, rsyslog ...

!SLIDE 

# Capistrano

!SLIDE commandline

    $ cap deploy

     * == Currently executing `deploy'
     * == Currently executing `deploy:update'
    ** transaction: start
     * == Currently executing `deploy:update_code'
       updating the cached checkout on all servers
       executing locally: "git ls-remote git://github.com/agilasverige/agilasverige_site.git master"
       command finished in 542ms * executing "if [ -d /home/agilasverige/apps/agilasverige/shared/cached-copy ]; then cd /home/agilasverige/apps/agilasverige/shared/cached-copy && git fetch -q origin && git reset -q --hard 93bd8a8277426d5ccdb94399704ee004a6050189 && git clean -q -d -x -f; else git clone -q git://github.com/agilasverige/agilasverige_site.git /home/agilasverige/apps/agilasverige/shared/cached-copy && cd /home/agilasverige/apps/agilasverige/shared/cached-copy && git checkout -q -b deploy 93bd8a8277426d5ccdb94399704ee004a6050189; fi"
       servers: ["agilasverige.cust.globalinn.com"]
       [agilasverige.cust.globalinn.com] executing command
       command finished in 1603ms
    [...]
    Recorded deployment to 'Agila Sverige' (2011-04-04 09:59:53 +0200)
    ** Uploaded deployment information to New Relic
      * == Currently executing `deploy:restart'
      * executing "touch /home/agilasverige/apps/agilasverige/current/tmp/restart.txt"
        servers: ["agilasverige.cust.globalinn.com"]
        [agilasverige.cust.globalinn.com] executing command
        command finished in 248ms
