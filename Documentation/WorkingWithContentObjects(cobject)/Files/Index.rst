.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../Includes.txt


.. _contentobjects-files:
*****
FILES
*****

This content object was integrated with the File Abstraction Layer (FAL) and is there to output information about files.

   Note: Do not mix this up with the cObject FILE; both are different cObjects.

The basic setup for FILES is as follows

::

   elements.myFiles = FILES
   elements.myFiles {

           // Source definition

           // Sorting

           renderObj = [SOME_CONTENT_OBJECT]
           renderObj {
                   // Rendering definition of the files
           }
   }


Source definition
=================

At the source definition we declare where the files have to come from. Are we getting files directly by it's UIDs
(“*files*”), are we using references (“*references*”), do we take files from a folder (“*folder*”), or is there a file
collection we can use (“*collection*”)? The source definition can be a combination more than one of these.


files (string/stdWrap)
----------------------

Comma-separated list of sys\_file UIDs, which are loaded into the FILES object.

::

   elements.myFiles = FILES
   elements.myFiles {

           files = 12,15,16

           renderObj = [SOME_CONTENT_OBJECT]
           renderObj {
                   // Rendering definition of the files
           }
   }


references (string /stdWrapor array)
------------------------------------

Provides a way to load files from a file field (of type IRRE with sys\_file\_reference as child table). You can either
provide a UID or a comma-separated list of UIDs from the database table sys\_file\_reference or you have to specify a
table, UID and field name in the according sub-properties of "*references*". When the rendering takes place within a
certain object, like page or content object, and you want to have the files from this object, the only property to be
mentioned is the “*fieldName*”.


By UIDs from the database table sys\_file\_reference
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

   elements.myFiles = FILES
   elements.myFiles {

           references = 27,28

           renderObj = [SOME_CONTENT_OBJECT]
           renderObj {
                   // Rendering definition of the files
           }
   }


Fetching all relations to the image field of a tt\_content record
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

   elements.myFiles = FILES
   elements.myFiles {

           references {
                   table = tt_content
                   uid = 34
                   fieldName = image
           }

           renderObj = [SOME_CONTENT_OBJECT]
           renderObj {
                   // Rendering definition of the files
           }
   }


Fetching all items related to the current page media field
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When this is rendered while in the page object, only the fieldName has to be filled. The table name and the UID will be
fetched from the current object.

::

   elements.myFiles = FILES
   elements.myFiles {

           references {
                   fieldName = media
           }

           renderObj = [SOME_CONTENT_OBJECT]
           renderObj {
                   // Rendering definition of the files
           }
   }


Fetching all items related to the current page media field while in another object
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

   elements.myFiles = FILES
   elements.myFiles {

           references {
                   table = pages
                   uid.data = tsfe:id
                   fieldName = media
           }

           renderObj = [SOME_CONTENT_OBJECT]
           renderObj {
                   // Rendering definition of the files
           }
   }


Fetching all items by levelmedia
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The data type of references is stdWrap, so we can getthe content of the pages media field in a certain level, not only
the current page. The “*slide*” parameter forces a walk to the bottom of the rootline until there's a "true" value to
return.

::

   elements.myFiles = FILES
   elements.myFiles {

           references {
                   data = levelmedia:-1, slide
           }

           renderObj = [SOME_CONTENT_OBJECT]
           renderObj {
                   // Rendering definition of the files
           }
   }


collections (string/stdWrap)
----------------------------

Comma-separated list of sys\_file\_collection UIDs, which are loaded into the FILES object.

::

   elements.myFiles = FILES
   elements.myFiles {

           collections = 41,49

           renderObj = [SOME_CONTENT_OBJECT]
           renderObj {
                   // Rendering definition of the files
           }
   }


folders (string/stdWrap)
------------------------

Comma-separated list of combined folder identifiers which are loaded into the FILES object.

A combined folder identifier looks like this:
::

   [storageUid]:[folderIdentifier]


The first part is the UID of the storage and the second part the identifier of the folder. The identifier of the folder
is often equivalent to the relative path of the folder.

::

   elements.myFiles = FILES
   elements.myFiles {

           folders = 2:my_pics/,4:my_images/

           renderObj = [SOME_CONTENT_OBJECT]
           renderObj {
                   // Rendering definition of the files
           }
   }


Combining them all
------------------

It's possible to combine different source definitions together.

::

   elements.myFiles = FILES
   elements.myFiles {

           files = 12,15,16
           references = 27,28
           collections = 41,49
           folders = 2:my_pics/,4:my_images/

           renderObj = [SOME_CONTENT_OBJECT]
           renderObj {
                   // Rendering definition of the files
           }
   }


sorting (string/stdWrap)
========================

Files can be sorted by using the sorting property. Sorting can be done on all kind of fields which are available within
the file object.

::

   elements.myFiles = FILES
   elements.myFiles {

           files = 52,55,56

           sorting = title

           renderObj = [SOME_CONTENT_OBJECT]
           renderObj {
                   // Rendering definition of the files
           }
   }


renderObj
=========

The cObject used for rendering the files. It is executed once for every file.

Note that during each execution you can find information about the current file using the getText property "*file*" with
the "*current*" keyword.

In the register there are two values available:

* **FILES\_COUNT** – The amount of files found within the source definition.
* **FILE\_NUM\_CURRENT** – The number of the current file.

You can use optionSplit within renderObj to allow different settings per file.


Rendering an image
------------------

::

   elements.myFiles = FILES
   elements.myFiles {

           files = 69,78,87

           renderObj = IMAGE
           renderObj {
                   file {
                           import {
                                   data = file:current:publicUrl
                           }
                   }
                   titleText {
                           data = file:current:title
                   }
           }
   }


Using optionSplit for a wrap
----------------------------

::

   elements.myFiles = FILES
   elements.myFiles {

           files = 69,78,87

           renderObj = IMAGE
           renderObj {
                   file {
                           import {
                                   data = file:current:publicUrl
                           }
                   }
                   titleText {
                           data = file:current:title
                   }
                   wrap = <div class="first">|</div> |*| <div class="middle">|</div> |*| <div class="last">|</div>
           }
   }


Making a typolink
-----------------

::

   elements.myFiles = FILES
   elements.myFiles {

           files = 92,94,96

           renderObj = IMAGE
           renderObj {
                   file {
                           import {
                                   data = file:current:publicUrl
                           }
                   }
                   stdWrap {
                           typolink {
                                   parameter {
                                           data = file:current:publicUrl
                                   }
                           }
                   }
           }
   }


Defining a maximum width
------------------------

::

   elements.myFiles = FILES
   elements.myFiles {

           files = 92,94,96

           renderObj = IMAGE
           renderObj {
                   file {
                           import {
                                   data = file:current:publicUrl
                           }
                           maxW = 200
                   }
           }
   }


Using the register value FILE\_NUM\_CURRENT
-------------------------------------------

::

   elements.myFiles = FILES
   elements.myFiles {

           files = 92,94,96

           renderObj = COA
           renderObj {
                   10 = IMAGE
                   10 {
                           file {
                                   import {
                                           data = file:current:publicUrl
                                   }
                           }
                   }
                   20 = TEXT
                   20 {
                           data = register:FILE_NUM_CURRENT
                           wrap = <p>Current file number: |</p>
                   }
           }
   }

.. toctree::
	:maxdepth: 5
	:titlesonly:
	:glob:

	FileStorage/Index
	Page/Index
	ContentObject/Index

