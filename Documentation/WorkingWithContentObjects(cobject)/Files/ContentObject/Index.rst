.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


.. _contentobjects-files-contentobject:
*********************
From a content object
*********************

When calling the FILES object when withing a certain content object, only the “*fieldName*” has to be entered in
“*references*”. The FILES object is aware what the current content object is (content or page).

::

   tt_content.myContentObject = FILES
   tt_content.myContentObject {

           references {
                   fieldName = image
           }

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

