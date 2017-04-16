Silent installation
-------------------

Silent installation of Miniconda or Anaconda can be used for deployment or testing or building services such as Travis CI and
Appveyor. In silent mode, screen prompts are not shown on screen and default settings are automatically accepted.

NOTE: These instructions are written for Miniconda, but you can substitute "Anaconda" if you are using that version.

We recommend starting with the latest version of Miniconda or Anaconda. Check to be sure your version
is up to date with a simple:

.. code-block:: console

    conda update conda


Windows
~~~~~~~

The Windows installer of Miniconda can be run in silent mode using
the ``/S`` argument. The following optional arguments are supported:

- ``/InstallationType=[JustMe|AllUsers]``, default: ``JustMe``
- ``/AddToPath=[0|1]``, default: ``1``
- ``/RegisterPython=[0|1]``, make this the system's default Python, default: ``0`` (Just me), ``1`` (All users)
- ``/S``
- ``/D=<installation path>``

All arguments are case-sensitive. The installation path must be the last
argument and should **NOT** be wrapped in quotation marks. When using silent 
installation with ``/S`` you must also specify a destination installation path 
with ``/D``.

The following command installs Miniconda for the current user without
registering Python as the system's default:

.. code-block:: bat

    start /wait "" Miniconda4-latest-Windows-x86_64.exe /InstallationType=JustMe /RegisterPython=0 /S /D=%UserProfile%\Miniconda3


Linux and OS X
~~~~~~~~~~~~~~

Silent installation of Miniconda for Linux and OS X is a simple as specifying the ``-b`` and ``-p`` arguments of the
bash installer. The following arguments are supported:

- ``-b``, batch mode, no PATH modifications to ``~/.bashrc``
- ``-p``, installation prefix/path
- ``-f``, force installation even if prefix ``-p`` already exists

Batch mode assumes that you agree to the license agreement, and it does not
edit the .bashrc or .bash_profile files.

A complete example:

.. code-block:: bash

    wget http://repo.continuum.io/miniconda/Miniconda3-3.7.0-Linux-x86_64.sh -O ~/miniconda.sh
    bash ~/miniconda.sh -b -p $HOME/miniconda
    export PATH="$HOME/miniconda/bin:$PATH"

NOTE: This only sets the PATH for the current session, not permanently. Trying
to use conda when conda is not in your PATH will cause errors such as "command
not found".

We recommend running ``source $HOME/miniconda3/bin/activate`` in each new
bash session before using conda, which will set the PATH and run the activation
scripts of your conda packages. Replace ``$HOME/miniconda3/bin/activate``
with the path to the activate script in your conda installation.

It is also possible to set the PATH permanently by adding a line to your
``.bashrc`` file such as ``export PATH="$HOME/miniconda3/bin:$PATH"``.
However, this makes it possible to use conda without running the activation
scripts of your conda packages, which may produce errors.
