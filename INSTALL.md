To begin with, you need to install the XHProf extension. Refer to the [PHP documentation](http://www.php.net/manual/en/xhprof.setup.php) if you need assistance.

You will need to manually create the database and populate it with the provided scheme. The database scheme is located at `/setup/database.sql`.

Rename the `/xhprof/includes/config.inc.sample.php` to `/xhprof/includes/config.inc.php`. There are only two supported parameters.

* `xhprof_url` is the URL to the XHProf.io library.
* `pdo` is the PDO instance. This library uses [PDO](http://uk3.php.net/pdo) to handle all of the database operations.

For XHProf.io to start collecting data, you need `/inc/prepend.php` included to every file of interest. The recommended approach is to update your `php.ini` configuration to automatically prepend this file.

    ; Automatically add files before PHP document.
    ; http://www.php.net/manual/en/ini.core.php#ini.auto-prepend-file
    ; This can also be done on a per-directory basis (.htaccess) or per-site (httpd.conf)
    ; http://www.electrictoolbox.com/php-automatically-append-prepend/
    auto_prepend_file = /[absolute path to xhprof.io]/inc/prepend.php

If you are using PHP-FPM, then XHProf.io will utilise `fastcgi_finish_request` to hide any overhead related to data collection. There is nothing to worry about if you are not using PHP-FPM either, as the overhead is less than a few milliseconds.

MySQL configuration
===================

This app uses InnoDB tables, therefore make sure you adjusted the corresponding mysql configuration (my.cnf) to some proper values.
For beginners see e.g. http://www.mysqlperformanceblog.com/2007/11/01/innodb-performance-optimization-basics/ for an initial setup.


Graphviz
========

To generate proper call graphs you need to install the `dot` binary.

see http://www.graphviz.org/Download..php or http://chocolatey.org/packages/Graphviz for windows.
