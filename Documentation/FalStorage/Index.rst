.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../Includes.txt


.. _falstorage:
***********
FAL Storage
***********

As you will probably know, the handling of files has drastically changed in TYPO3 CMS since the introduction of the File
Abstraction Layer. Files are no longer handled by its path and name, like "``/fileadmin/user_upload/images/my_image.png``"
, but with records in the database.


.. _falstorage-files:
Files
=====

When uploading a file in the TYPO3 backend, the file will get indexed. The file information is extracted and stored as a
record in the database in the table “*sys\_file*”.


.. _falstorage-references:
References
==========

When adding file objects to content objects using media fields, like “*Text with Image*”, “*Image*” or “*Media*”, or a page,
the paths of the selected images (or other media) were stored comma-separated in the database.

With the introduction of FAL, references are stored to such a file using the table “*sys\_file\_reference*”. In the image
field of the content object only the amount of references is stored. This means if we want to render an image from such
a field, we need to make clear references are used.


.. _falstorage-filecollections:
File Collections
================

With a file collection you can group files by making a static collection of files, selected by their UIDs, or by
selecting a (directory of a) file storage. File collections are stored in the database table "*sys\_file\_collection*".


.. _falstorage-folders:
Folders
=======

Folders are a representation of a File Storage. A File Storage could be a local filesystem, but also a remote one. File
Storages can be defined in the backend. A folder in FAL is not directly a folder of the local filesystem, but a folder
within a File Storage. Folders can be identified by its File Storage UID and the folder identifier (which is a path
within the File Storage).

::

   [storageUid]:[folderIdentifier]

