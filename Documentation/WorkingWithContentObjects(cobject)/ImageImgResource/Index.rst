.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../Includes.txt


.. _contentobjects-imageimgresource:
*********************
IMAGE / IMG\_RESOURCE
*********************

These content objects should be familiar to you. They have been around for quite some time. “IMAGE” returns an image tag
with the image file, defined in the property “file”, and is processed according to the properties set. “IMG\_RESOURCE”
only returns the image-reference, the path and name where the image is located. It also uses the same property “file”.

The property “file” is important here. According to the document “TypoScript Reference” (
`http://docs.typo3.org/typo3cms/TyposcriptReference/ <http://docs.typo3.org/typo3cms/TyposcriptReference/>`_ ), this
property is of the data type “imgResource” as mentioned earlier in this document.

.. toctree::
	:maxdepth: 5
	:titlesonly:
	:glob:

	FileStorage/Index
	Page/Index
	ContentObject/Index

