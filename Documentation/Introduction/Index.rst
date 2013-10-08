.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../Includes.txt


.. _introduction:
************
Introduction
************

With the release of TYPO3 version 6.0 the File Abstraction Layer (FAL) was introduced. This changes the way how image
files can be accessed. Image files are now records which can be referred to in various places. Instead of using a file
directly, TYPO3 now uses these file records or uses a reference to them.

This documents describes how to handle FAL records in TypoScript.