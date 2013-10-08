.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../Includes.txt


.. _fields:
******
Fields
******

TYPO3 is returning the values of fields to TypoScript, when calling a page or content element. The values of these
fields (most likely the content in the database) can be used for your own TypoScript needs.

For instance we want to display the title of a page. This can be done by making a TEXT content object which is using the
field “*title*”.

::

   elements.pageTitle = TEXT
   elements.pageTitle {
           field = title
   }

Since the introduction of FAL, you would expect that the media fields of pages (field “*media*”) and tt\_content objects
(fields “*media*” and “*image*”) contain the reference UIDs. But this is not true.

In the database these fields only contain the number of files which are attached to this field.

When working in TypoScript these fields contain a relative path (from “``/uploads/media/``”) to the media files, or images,
comma-separated. The reason for this is backwards compatibility.

Two more fields are introduced in “*pages*” and “*tt\_content*”. These fields are not present in the database, but are added
when the records are retrieved from the database. The names of these field depend on the original name of the field
which contains the references.


.. _fields-media:
media
=====

* **media\_fileReferenceUids** - Contains the UIDs of the file referencerecords, comma-separated.
* **media\_fileUids** - Contains the UIDs of the file records, comma-separated.


.. _fields-image:
image
=====

* **image\_fileReferenceUids** - Contains the UIDs of the file reference records, comma-separated.
* **image\_fileUids** - Contains the UIDs of the file records, comma-separated.


   These field additions are **only** done for the “*pages*” field “*media*” and the “*tt\_content*” fields “*image*”
   (when the cType is “*image*” or “*textpic*”) and “*media*” (when the cType is “*uploads*”).

