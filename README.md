# Apache 2 LESS handler

## Overview
The purpose is to have Apache handle serving LESS documents. This allows LESS to be served directly by the server without the need to compile manually. LESS is compiled on the server using node.js and lessc. The compiled files are cached in the temporary directory and then passed through to the browser. Compiled code is returned as text/css.


### Error Handling
When an error occurs while compiling the server will return a 500 status code and the STDERR output from the lessc command as text/plain.


### Options
There are several query string flags that can be set to perform some specific tasks.

- **recache**
    * Forces recompile and caching of a given file.
    * example: *http://example.com/styles.less?recache*
- **nocache**
    * Bypasses caching and returns compiled output. This is significantly less scalable than serving cached files. Typically this is used while development is occurring.
    * example: *http://example.com/styles.less?nocache*
- **nocompile**
    * Returns the uncompiled LESS file.
    * example: *http://example.com/styles.less?nocompile*

##Installation

### Requirements
- Apache 2.2.x
- PHP 5.x
- nodejs >= 6.x
- less >= 1.x

###Fedora / CentOS / RHEL

Execute the following with root permissions i.e. sudo.

    rpm --import http://nodejs.tchol.org/RPM-GPG-KEY-tchol
    yum localinstall --nogpgcheck http://nodejs.tchol.org/repocfg/fedora/nodejs-stable-release.noarch.rpm
    yum install nodejs npm
    npm install -g less
    ln -svf /usr/lib/node_modules/less/bin/lessc /usr/bin/lessc
    ln -svf /usr/bin/nodejs /usr/bin/node

    cp ./less.conf /etc/httpd/conf.d/less.conf
    cp -r ./less-compiler /etc/httpd/conf.d/

### Debian / Mint / Ubuntu

Execute the following with root permissions i.e. sudo.

    apt-get install python-software-properties
    add-apt-repository ppa:chris-lea/node.js
    apt-get update
    apt-get install nodejs npm
    npm install -g less

    cp less.conf /etc/apache2/conf.d/less.conf
    cp -r ./less-compiler /etc/apache2/conf.d/

