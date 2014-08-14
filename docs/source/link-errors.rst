===========
Link Errors
===========

Table of contents:
==================

#. :ref:`broken`
#. :ref:`external`
#. :ref:`common-issues`
#. :ref:`related-settings`

.. _broken:

Broken linkages
===============

What is a broken linkage?
-------------------------

A broken linkage is when a program or a shared library is trying to link against a library that it can't find.

On linux, you can use the program ``ldd`` to inspect what shared libraries something is trying to link against.  A broken linkage might look something like this

.. code-block:: bash

    $ ldd libzmq.so
    linux-vdso.so.1 =>  (0x00007fffbbbfe000)
    libsodium.so.4 => not found
    librt.so.1 => /lib/x86_64-linux-gnu/librt.so.1 (0x00007f7c1d8a9000)
    libpthread.so.0 => /lib/x86_64-linux-gnu/libpthread.so.0 (0x00007f7c1d68a000)
    libstdc++.so.6 => /usr/lib/x86_64-linux-gnu/libstdc++.so.6 (0x00007f7c1d386000)
    libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f7c1cfc0000)
    libgcc_s.so.1 => /lib/x86_64-linux-gnu/libgcc_s.so.1 (0x00007f7c1cda9000)
    /lib64/ld-linux-x86-64.so.2 (0x00007f7c1dd0f000)
    libm.so.6 => /lib/x86_64-linux-gnu/libm.so.6 (0x00007f7c1caa3000)

Note the ``not found`` value for the libsodium.so entry

A valid entry might look like

.. code-block:: bash

    libsodium.so.4 => /home/builder/anaconda/envs/_build/lib/./libsodium.so.4 (0x00007f6ab95a5000)

What causes broken linkages?
----------------------------

Badness

How to fix broken linkages
--------------------------

magic

.. _external:

External linkages
=================

What is an external linkage?
-----------------------------

An external linkage is when a shared library exists on your system but outside of the build/test directory.

If you build root was ``/home/builder/anaconda/envs/_build/``, then all the libraries listed in the ldd example above would be external linkages.

What causes external linkages
-----------------------------

An external linkage implies that the recipe does not provide a library.  The system falls back to its ``<SOMETHING>_PATH`` and links to dependent libraries it finds there.

How to fix external linkages
----------------------------

**An external linkage doesn't necessarily have to be fixed**: The built package will likely work fine on the system it was built on.

In fact, some system libraries currently do not have a conda recipe and therefore must already live somehwere on your system.  DynamicLibrary's `allowed_outside <https://github.com/conda/conda-build/blob/0cd18c5e51a741a5b7d05d63ad10f13e2aab7c32/conda_build/dll.py#L842-L850>`_ method permits common libraries to live outside of the build root **without** creating an external linkage warning.

You can squelch external linkage messages by adding elements to the ``extra_external`` section of your build recipe.

However, external linkages **should** be fixed if you want to distribute the built package.

To fix external linkages ...

.. _common-issues:

Common issues
=============

Some common issues are

#. A library is both a ``build`` **and** a ``run`` requirement but is only added as a ``build`` requirement.  Common examples are

   #. building with gcc but not realizing that libgcc is linked against

   #. libgfortran

#. Common issue 2

.. _related-settings:

Linkage related settings
========================

#. allow_x11
#. extra_external
#. forgiving
#. allow_somethign_or_other
