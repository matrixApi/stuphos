Copyright 2009-2022 runphase.com
================================

Virtualizes python so that it is isolated and controlled in terms of resource usage per
registered user account, and all operations are tracked by time, generating computational
telemetry and executive control.


Intended Audiences
==================

* System administrators who want to support user multitasking without system management
  overhead.
* Web administrators who want to publish a CMS site with integrated real-time networking.
* Physical and computational scientific research.  Python 3 users.


Legal and Operational Notes
===========================

This software makes use of cryptographic algorithms, designed to protect the user data
and the user, but may be restricted in jurisdictions that overrule their use.

Please research the full law regarding data and information security.

THERE IS ABSOLUTELY NO WARRANTY INCLUDED.


Starting
========

Unpack the skeletoncore.tar.gz directory and configure it for your application (the
location of the stuphos packages in your PYTHONPATH), then switch to that directory
and run it like this: ./runcore --headless &

Connect to it with a web browser.


Boot Procedure
==============

An embedding core invokes the boot start and complete routines in the mud module to
initialize the bindings and runtime.

These things start up in the application, opening up all components and facilities.

    * Registry is configured
    * Site packages are loaded
    * Event bridge module is constructed and initialized
    * VM, system journal installed
    * System package paths are installed
    * Environment updated
    * XMLRPC host started
    * Management components
        * Web Adapter Session Manager
        * WSGI Webserver

    * Facilities
    * Zones
    * Commands
    * Warmboot
    * Engine Loop


Application & Core Architecture
===============================

The system uses a collection of components to build its application of managing objects.
One of the components is the 'registry' which names unique objects within the runtime,
and requires that it be installed during boot time (this is normally handled by the
boot procedure).

Other component package implementations are configured using the 'components.pth' file
for service implementations, external (third-party) server package installations, and
developmental modules.


Supplemental
============

With an extended license, the 'ph' package contains a virtual machine computational
core and database querying engine.

The 'stuphmud' package contains code previously released in ''stuphos-lite''.


Filesystem and Command-Line Configuration
=========================================

Options:
    -w --world-dir                          path
    -z --zone-index --index                 string
    -i --interactive                        bool
    -a --async                              bool
    -W --cascade --load-world               bool
    -C --config-file --config --game-config path
    -g --debug                              count
    -n --no-world                           bool
    -p --port                               integer
    -m --mud-package --mud                  string
    -s --supreme                            bool
    --admin-name                            string
    --enter-game                            bool
    -L --data-dir --lib-dir                 path
    -v --verbose                            count
    --headless --no-console                 bool

Experimental:
    --blocking                              integer
    --runpid                                bool


The configuration file has the following options:

    [MUD]
    config-dir = .
    components: components.pth
    traceback-relative: yes
    log-uncaught-traceback: yes
    logindent = 4
    greetings: name prompt %w means whitespace
    greeting-delay: 1.2
    http-redirect-url: https://runphase.com:2180/
    player-store-shelf = %(config-dir)s/.players.shelf
    zone-config-file = .zone-modules.cfg
    world-path = ../../lib/archive/lib/world
    olc-world-path = ../../lib/archive/lib/world
    zone-database: sqlite


    [Management]
    embedded-webserver: yes
    pentacle-service: no
    session-adapter: yes
    system-shell: no
    subdaemon-manager: no
    syslog-scanner: no


    [XMLRPC]
    off: off
    address: 0.0.0.0
    ; certificate-path = server.pem


    [Security]
    trust-localhost: yes
    ; trusted-domain: 10.0.0.1


    [Interpreter]
    rich-editor: yes
    player-notebook: yes
    wizard-gc: yes
    checkpointing: no
    native-traceback: yes ; no


    [Environment]
    PENTACLE_PARTNER_NAME = 'stuphos/mud'


    [Syslog]
    path.1: ..\log\syslog*
    path.2: mattercore.run.log
    patterns: etc\syslog-patterns.cfg


    [Services]
    facility.billing: ph.emulation.billing.BillingCore


    [DjangoService]
    port = 2180
    database = sqlite
    sitemap = stuphos.webserver.project.urls
    show-debug-page = admin
    certificate-path = server.pem
    software: phaseware
    log-request: yes
    hosts:
        <public ip address 1>
        <hostname 1>
        <hostname 2>
        ...
    media:
        serving-path: folder-path
    webapps:
        person.services.web
        ...

    [DBCore]
    primary.type = pg-auth
    primary.path = ../lib/db.conf ; username\npassword\n
    primary.host = 127.0.0.1
    primary.port = 5432
    sqlite.type = sqlite
    sqlite.path = sqlite:webcore.db
    sqlite.file-path = webcore.db


    [SystemComponents]
    system-path.common: /workspace/library/packages/common

    [SystemPackages]
    package.wrlc: op

    [Logging]
    database: sqlite

    [Billing]
    policy-rates-path = ../resources/rates.wmc



Web Interface Guide
===================

The application is developed internally by programming principals, which require user
authentication.  Programming documentation should be viewable within the online interface.

