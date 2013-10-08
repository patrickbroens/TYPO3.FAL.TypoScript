.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


.. _contentobjects-imageimgresource-page:
***********
From a page
***********

In TypoScript you can retrieve the content of a field using different methods. It's possible to get the field content
from the current page, or by using the “*getText*” data type, which allows you for instance to walk to the bottom of the
rootline until a value has been found.


Using fields from the current page
==================================

As described in the part “Fields” we have the following fields we can use:


media
-----

For backwards compatibility the content of this field is the relative path to the media elements, like images, based on
/uploads/media/ (like it was in the old days). The resources are comma-separated. The path to an image looks like
“``../../fileadmin/user\_upload/images/my\_image.jpg``”.

::

   elements.image = IMAGE
   elements.image {
           file {
                   import = /uploads/media/
                   import {
                           field = media
                           listNum = 0
                   }
           }
   }

This seems odd. The directory “``/uploads/media/``” is not in use anymore. Like mentioned above this is done for
backwards compatibility. In the import property you can put everything you want, as long as it covers two directories.
“``/foo/bar/``” is also possible, for instance. Keep in mind that the “import” property should be there, otherwise the
path to the image is calculated wrong and you end up with nothing.


media\_fileUids
---------------

Contains the UIDs of the file records, comma-separated.

::

   elements.image = IMAGE
   elements.image {
           file {
                   import {
                           field = media_fileUids
                           listNum = 0
                   }
           }
   }

Since the file property can be an integer as well, the UID of the first file is used here.


media\_fileReferenceUids
------------------------

Contains the UIDs of the file reference records, comma-separated.

::

   elements.image = IMAGE
   elements.image {
           file {
                   import {
                           field = media_fileReferenceUids
                           listNum = 0
                   }
                   treatIdAsReference = 1
           }
   }

Here the first file reference UID is used. Make sure you tell the imgResource that the UID which is used is a reference
with the property “*treatIdAsReference*”.


Using the getText levelmedia property
=====================================

The levelmedia property gets the content of the pages media field in a certain level. The “*slide*” parameter forces a
walk to the bottom of the rootline until there's a "true" value to return.

::

   elements.image = IMAGE
   elements.image {
           file {
                   import {
                           data = levelmedia: -1,slide
                           listNum = 0
                   }
                   treatIdAsReference = 1
           }
   }

