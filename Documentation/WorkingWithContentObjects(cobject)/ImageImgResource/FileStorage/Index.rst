.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


.. _contentobjects-imageimgresource-filestorage:
**************************
From File Storage directly
**************************


Using a path
============

In previous versions of TYPO3, you could simply refer to an image by using the path and name, like

::

   element.image = IMAGE
   element.image {
           file = /fileadmin/user_upload/images/my_image.jpg
   }

As :ref:`mentioned <fields>` before, it's not advisable anymore, especially when using a “File Storage” which is not on the local
filesystem.


Using the id of the sys\_file record
====================================

It is advisable to use the id of the sys\_file record like this:

::

   element.image = IMAGE
   element.image {
           file = 9999
   }

The property “file” has become an integer and corresponds with the UID of the record in the table “*sys\_file*”.


Using the id of a file reference
================================

You can also use a reference here from the table “*sys\_file\_reference*”, although I don't see why you would need this
in the situation below.

In the data type “*file*” a new property “*treatIdAsReference*” has been added, which is of the data type “*boolean*”.
If set, given UIDs are interpreted as UIDs to “*sys\_file\_reference*” instead of “*sys\_file*”. This allows using file
references:

::

   element.image = IMAGE
   element.image {
           file = 9999
           file {
                   treatIdAsReference = 1
           }
   }

