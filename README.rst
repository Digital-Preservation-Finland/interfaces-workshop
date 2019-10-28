Interfaces workshop - october 2019
==================================

This repository contains test scripts and command examples for the interfaces
training day held in October 2019 at CSC.

Installation of the bash scripts
--------------------------------

Bash scripts are used in the fourth excercise. Install and run the bash scripts
like this::

    cd bin
    chmod u+x <script filename>
    ./<script filename>

Test cases commands
-------------------

Open the test case .rst files for specific command instructions for each of the
six test cases with your browser by clicking the corresponding link.

Using curl and jq
-----------------

The `curl`_ is a command line tool for transfering data with URLs. Curl is used
in this workshop with a few parameters. The full list can be used using the
command::

    curl -h

.. _curl: https://curl.haxx.se/

These parameters are used:

    * -s silent mode, outputs only the response body
    * -k insecure, since the test server doesn't contain a real cert
    * -u user, adds the user name to the request
    * -X command, for adding POST methoid to the disseminate requests
    * -o output, when saving the DIP as a file

In addition, `jq`_ is used for most commands to parse the json response to a more
readable mode.

.. _jq: https://stedolan.github.io/jq/

The test data set and testing server
------------------------------------

For this workshop, a test server is set up containing test data. This test server
will only be open during the workshop, but the example commands and
scripts in this repository can be configured to work with real servers and
credentials.

The test data is described using Dublin Core. This is further explained in the
excercises.
