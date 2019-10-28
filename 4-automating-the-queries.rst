The REST API is meant for automated processing
==============================================

The REST API is a machine interface meant for automated processing between
systems. The queries are chained, meaning that the results for a query contain
URLs to following queries, e.g. the search query contain URLs to the management
of each AIP in the search results and the AIP management result contains a URL
for posting a disseminate request and so on.

The polling of the completed DIP can also be automated and the DIP can be
downloaded automatically when it is ready.

A simple polling of a DIP can be done e.g. with this command::

    watch -n 5 curl -sku training "https://86.50.170.64/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/disseminated/8fa5008f-350f-4444-bbf2-4ae240073f29"

In this excercise module the included shell scripts are meant to be utilized and
can be further developed if necessary. 

The scripts
===========

Installation of the bash scripts
--------------------------------

Install and run the bash scripts like this::

    cd bin
    chmod u+x <script filename>
    ./<script filename>

pas-rest
--------
A simple script that just adds the curl command, the base URL and the login
credentials. The script needs the URL for the resource, e.g.::

    pas-rest <password> /api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/search

loop-search
-----------
A script that lists all AIPs and loops through all pages while doing so::

    loop-search <password>

loop-preserved
--------------
A script that loops all AIPs and performs the manage AIP command for each found
package (``GET <base>/<contract>/preserved/<aip-id>``)::

    loop-preserved <password>

collect-aip-ids
---------------
A script that loops through all AIPs and returns a list of the AIP IDs::

    collect-aip-ids <password>

get-dip
-------
A script that submits a DIP request, polls the DPS for the DIP creation and finally
downloads the DIP as a file when it is ready::

    get-dip <password> /api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/disseminated/8fa5008f-350f-4444-bbf2-4ae240073f29

To specifiy the filename of the DIP, use it like this::

    get-dip <password> /api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/disseminated/8fa5008f-350f-4444-bbf2-4ae240073f29 mydip.zip

get-dip-metadata
----------------
Like the script above, but outputs the metadata (the mets.xml)::

    get-dip-metadata <password> /api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/disseminated/8fa5008f-350f-4444-bbf2-4ae240073f29

To save the metadata to a file::

    get-dip-metadata <password> /api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/disseminated/8fa5008f-350f-4444-bbf2-4ae240073f29 mets.xml


Further development
-------------------

The scripts can be modified to suit the needs of your organization, like the login
credentials.

What kind of scripts does your organization need in order to automate the management
of your preserved contents? Outline the idea for scripts or their intended functions.

How does your backend system communicate with the DPS?
