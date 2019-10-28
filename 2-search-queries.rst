The Search Query Syntax
=======================

Searching for packages is done by quering for the contents of the METS document. 
The queries use key:value pairs, where the key is the element name in the METS
document and the value is the contents of the element. The query uses the `Apache
Lucene syntax`_.

.. _Apache Lucene syntax: https://lucene.apache.org/core/3_6_0/queryparsersyntax.html

The Basic Query
---------------

The METS OBJID is the ID that is given to a SIP by the organization. In order to
find the corresponding AIP from the Digital Preservation System, the ID can be
used to retrieve the AIP. For example, we know that we sent a SIP with the ID
``fbf9d109-545c-43c1-af06-287b829d1705`` and would like to retrieve it.

1) Retrieve an AIP by its OBJID::

    curl -sku training "https://86.50.170.64/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/search?q=OBJID:fbf9d109-545c-43c1-af06-287b829d1705" | jq

Search by the description of the content
----------------------------------------

The test data is described using the `Dublin Core`_ metadata standard. The Dublin
Core elements are as follows:

    * contributor
    * coverage
    * creator
    * date
    * description
    * format
    * identifier
    * language
    * publisher
    * relation
    * rights
    * source
    * subject
    * title
    * type

.. _Dublin Core: https://www.dublincore.org/specifications/dublin-core/

2) Search for all AIPs::

    curl -ku training "https://86.50.170.64/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/search?q=*:*

The search query ``*:*`` returns all AIPs for a contract.

3) Search for AIPs with a coverage description::

    curl -ku training "https://86.50.170.64/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/search?q=coverage:*" | jq

Searching for a ``key:*`` returns all AIPs with data in the key element

4) Search for a specific creator::

    curl -sku training "https://86.50.170.64/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/search?q=creator:Westö

Searching for content type
--------------------------

Since the whole METS document is searchable, also technical metadata can be used
in the search. For example, file format based search is done by search for the
formatName element in the `PREMIS`_ metadata.

.. _PREMIS: https://www.loc.gov/standards/premis/

5) Search for all AIPs containing text data::

    curl -sku training "https://86.50.170.64/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/search?q=formatName:text" | jq

6) Search for AIPs containing images::

    curl -sku training "https://86.50.170.64/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/search?q=formatName:image" | jq

7) Search using a specific format::

    curl -sku training "https://86.50.170.64/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/search?q=formatName:application/pdf" | jq

Using Boolean Operators
-----------------------

The Apache Lucene Syntax support using boolean operators in the query to search
for multiple conditions.

8) Search for books about Japan::

    curl -sku training "https://86.50.170.64/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/search?q=type:Text+AND+subject:Japani" | jq

9) Seach for books or Japan as the subject::

    curl -sku training "https://86.50.170.64/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/search?q=type:Text+OR+subject:Japani" | jq

Wildcards and fuzzy searches
----------------------------

10) Using wildcards to search for a string at the beginning of a word::

     curl -sku training "https://86.50.170.64/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/search?q=description:shakki" | jq

No wildcards return 0 results. But using a wildcard should return AIPs::

    curl -sku training "https://86.50.170.64/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/search?q=description:shakki*" | jq

11) Using fuzzy search to find strings close to the search term::

     curl -sku training "https://86.50.170.64/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/search?q=description:koti~" | jq

This doesn't seem right, adjusting the similarity ratio to be more strict should
do the trick::

    curl -sku training "https://86.50.170.64/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/search?q=description:koti~0.6" | jq
