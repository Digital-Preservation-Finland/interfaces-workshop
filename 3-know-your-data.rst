Getting to know your data
=========================

The point of this excercise is to use the REST queries in order to orient yourself
with the data and getting a good overview of the contents being preserved for
this test data set.

Using the pagination
--------------------

The REST API uses pagination to restrict the amount of results on one page, i.e.
in one query. The user can configure and navigate the pages using the parameters
``limit`` and ``page``.

1) Limit the search results to split the pages to several pages::

    curl -sku training "https://temp-course-instance/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/search?limit=5&page=1" | jq

Now we can see that the ``links`` key in the result contain a URL to the next page.

2) Display the results using the next page URL::

    curl -sku training "https://temp-course-instance/api/2.0/urn:uuid:68320fee-f361-4a21-aad1-282c2040b994/search?q=&limit=5&page=2" | jq


The test data - how is it described
-----------------------------------

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

Since the whole METS document is searchable, also technical metadata can be used
in the search. For example, file format based search is done by search for the
formatName element in the `PREMIS`_ metadata.

.. _PREMIS: https://www.loc.gov/standards/premis/

Getting an overview of the collection in the DPS
------------------------------------------------

The goal of this excercise is to use the REST commands to get an overview of 
the preserved data in the DPS. Use the statistics and search commands to answer
the following questions:

    * How many AIPs are stored in this collection?
    * How many AIPs are stored by each content type?
    * Which file formats does the collection contain?
    * What topics does the collection cover?
    * Which content type is the most common in the collection?
    * What are the OBJID:s of the preserved resources?

What information is most relevant for your organization when using the REST API
to search and manage the preserved contents?

Finding a specific AIP
----------------------

The goal is to find a specific AIP in the collection.

    * What is the title and mets:OBJID of the resource that mentions the word ``Halloween``?

