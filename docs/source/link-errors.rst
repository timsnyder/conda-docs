===========
Link Errors
===========

Table of contents:
==================

#. :ref:`broken`
#. :ref:`external`

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

What causes external linkages
-----------------------------

Badness

How to fix external linkages
----------------------------

magic
