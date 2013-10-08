.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../Includes.txt


.. _datatypesandfunctions:
************************
Data types and Functions
************************

A few TypoScript data types and functions have been changed to handle FAL records.

For image rendering mainly the imgResource data type and function are used. They have been adapted to accept properties
from FAL, like a UID of the FAL record or reference.

For all FAL objects some additional configuration is possible within the getText data type.


.. _datatypesandfunctions-imgresourcedatatype:
imgResource data type
=====================

The “*imgResource*” data type describes the path and name to an image, the “*resource*”, like
“``/fileadmin/user\_upload/images/my\_image.png``”

`http://docs.typo3.org/typo3cms/TyposcriptReference/DataTypes/Reference/Index.html#imgresource <http://docs.typo3.org/typo3cms/TyposcriptReference/DataTypes/Reference/Index.html#imgresource>`_

Previously the “*imgResource*” data type only accepted a path and name, a resource. Since FAL is working with records,
this does not make sense, although still possible. The “*imgResource*” data type accepts an integer as well. This integer
can be the UID of the FAL record you want to use, or the UID of the reference.

::

   element.image = IMAGE
   element.image {
           file = 9999
   }


.. _datatypesandfunctions-imgresourcefunction:
ImgResource function
====================

imgResource contains the properties that are used with the data type imgResource.

`http://docs.typo3.org/typo3cms/TyposcriptReference/Functions/Imgresource/Index.html <http://docs.typo3.org/typo3cms/TyposcriptReference/Functions/Imgresource/Index.html>`_

As mentioned above at the :ref:`imgResource data type <datatypesandfunctions-imgresourcedatatype>`, the data type accepts UIDs as well. This can be the UID of the
FAL record, or the UID of a reference. Because only an integer is used, the data type does not know if you are using
the UID of a file or reference. Therefor we need to make this clear to the data type.

A new property has been introduced to make this distinction: “*treatIdAsReference*”, which is of the data type “*boolean*”.
If set, given UIDs are interpreted as UIDs to “*sys\_file\_reference*” instead of to “*sys\_file*”.

::

   element.image = IMAGE
   element.image {
           file = 9999
           file {
                   treatIdAsReference = 1
           }
   }


.. _datatypesandfunctions-gettextdatatype:
getText data type
=================

The getText data type allows you to retrieve a value in a PHP array or object, which is not necessarily from the current
object you are working with, like the page.

`http://docs.typo3.org/typo3cms/TyposcriptReference/DataTypes/Reference/Index.html#gettext <http://docs.typo3.org/typo3cms/TyposcriptReference/DataTypes/Reference/Index.html#gettext>`_


file
----

A new property “*file*” has been added to the getText data type. This allows you to retrieve a property from a file object
(FAL) by identifying it through its sys\_file UID. The following syntax is used:

::

   file:[uid]:[propertyName]

* [uid] is the UID of the file object

* [propertyName] is the name of the property to retrieve

Note: During execution of the FILES cObject, you can also reference the current file with "*current*" as UID like

::

   file:current:size

With “*file*” you can access all properties from a file object.

The example below shows the “*title*” of a file object with the UID 9999.

::

   element.title = TEXT
   element.title {
           data = file:9999:title
   }


levelmedia
----------

The levelmedia property gets the content of the pages media field in a certain level. The behaviour of this property has
changed. It now returns the UIDs of file references, instead of comma-separated paths to images. Therefor you need to
use the “*treatIsAsReference*” property on an image resource when working with levelmedia.

