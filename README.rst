pylint-venv
===========

Pylint_ does not respect the currently activated virtualenv_ if it is not
installed in every virtual environment individually.  This module provides
a Pylint init-hook to use the same Pylint installation with different virtual
environments.

Installation
------------

.. code:: bash

    pip install pylint-venv

Add the following to your ``~/.pylintrc``:

.. code:: ini

    init-hook=
        try: import pylint_venv
        except ImportError: pass
        else: pylint_venv.inithook()

The hook will then be used automatically if

- a virtualenv is activated

- a Conda environment is activated

- no env is activated but your CWD contains a virtualenv in ``.venv``

and if pylint is not installed in that env, too.

You can also call the hook via a command line argument:

.. code:: console

    $ pylint --init-hook="import pylint_venv; pylint_venv.inithook()"

This way you can also explicitly set an environment to be used:

.. code:: console

    $ pylint --init-hook="import pylint_venv; pylint_venv.inithook('$(pwd)/env')"


In case Pylint is installed in a isolated virtualenv and not under a global python interpreter,
e.g. with pipx_ or pre-commit_,  call ``init_hook`` with ``force activation``:.


.. code:: python

    pylint_venv.inithook(force_activation=True)

Otherwise the hook will not work due to already be in a virtual environment.
.. _Pylint: http://www.pylint.org/
.. _virtualenv: https://virtualenv.pypa.io/en/latest/
.. _pipx: https://github.com/pipxproject/pipx/
.. _pre-commit: https://pre-commit.com/
