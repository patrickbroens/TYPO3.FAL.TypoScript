.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


.. _contentobjects-files-page:
*********************
From a page
*********************

When calling the FILES object when withing a certain content object, only the “*fieldName*” has to be entered in
“*references*”. The FILES object is aware what the current content object is (content or page).

::

   elements.myFiles = FILES
   elements.myFiles {

           references {
                   fieldName = media
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

