.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


.. _contentobjects-imageimgresource-contentobject:
*********************
From a content object
*********************


Fields from the core
====================

As described above in the chapter “Fields”, some transformation will be done for the default media fields in the cTypes
“*image*”, “*textpic*” and “*uploads*”. Two more fields are added to the content object, where the name depends on the
original field name.

* For the field “*media*” (only used in the cType “*uploads*”) we will get the two extra fieldsmedia\_fileReferenceUids
  and media\_fileUids.

* For the field “*image*” (used in the cTypes “*textpic*” and “*image*”) the two fields image\_fileReferenceUids and
  image\_fileUids will be added.

To use these fields, have a look at how it is done with the media fields of a page.


Additional fields from extensions
=================================

Additional fields from extensions will not be transformed like done with the core fields. They will always contain the
reference UIDs, comma-separated. This means, if the extension is using the right implementation in $TCA for FAL records.
For these you can always use

::

   tt_content.myContentObject = COA
   tt_content.myContentObject {
           10 < = lib.stdHeader

           20 = IMAGE
           20 {
                   file {
                           import {
                                   field = mySpecialImageField
                           }
                           treatIdAsReference = 1
                   }
           }
   }

