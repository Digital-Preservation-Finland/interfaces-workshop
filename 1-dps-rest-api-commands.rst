Digital Preservation Services REST API commands
===============================================

These command examples consist of the basic commands that is supported by the
REST API of the Finnish National Digital Preservation Services. The API is
documented `here`_.

.. _here: http://digitalpreservation.fi/specifications

The REST commands
-----------------

1) Display the statistics of a contract::

    curl -sku <username:password> "https://<testing-instance>/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/statistics/overview" | jq

2) List all AIPS::

    curl -sku <username:password> "https://<testing-instance>/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/search" | jq

3) Select an AIP from the list and display the management functions for an AIP::

    curl -sku <username:password> "https://<testing-instance>/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/preserved/training-kokoelma001-2.tar-a8bbd225-fbbd-47bc-8a89-e666ba6ed5d6.tar" | jq

4) Submit a request to disseminate the AIP, the request is a POST method::

    curl -sku <username:password> -X POST "https://<testing-instance>/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/preserved/training-kokoelma001-2.tar-a8bbd225-fbbd-47bc-8a89-e666ba6ed5d6.tar/disseminate" | jq

5) Poll the REST for the DIP package::

    curl -sku  <username:password> "https://<testing-instance>/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/disseminated/<dip-id>" | jq

6) Download the DIP package to a file::

    curl -sku <username:password> -o "dip.zip" "https://<testing-instance>/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/disseminated/7ac4f05c-6465-4c26-af71-c17d8c527809/download"

7) Download and display the DIP metadata, returns::

    curl -sku <username:password> "https://<testing-instance>/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/disseminated/7ac4f05c-6465-4c26-af71-c17d8c527809/metadata" 

8) Find an ingest report::

    curl -sku <username:password> "https://<testing-instance>/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/ingest/report/fbf9d109-545c-43c1-af06-287b829d1705" | jq    

9) Download the ingest report as XML::

    curl -sku <username:password> "https://<testing-instance>/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/ingest/report/fbf9d109-545c-43c1-af06-287b829d1705/training-sip-sound-003.tar-5af8f577-4a08-4b3c-99cb-1fd2be958e82?type=xml"
