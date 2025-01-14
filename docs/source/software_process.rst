..  _software_process:

================
Software Process
================

----------------------
Continuous Integration
----------------------

HDMF is tested against Ubuntu, macOS, and Windows operating systems.
The project has both unit and integration tests.

* `Azure Pipelines`_ runs all HDMF tests on Windows and macOS
* CircleCI_ runs all HDMF tests on Ubuntu

Each time a PR is published or updated, the project is built, packaged, and tested on all supported operating systems
and python distributions. That way, as a contributor, you know if you introduced regressions or coding style
inconsistencies.

There are badges in the README_ file which shows the current condition of the dev branch.

.. _CircleCI: https://circleci.com/gh/hdmf-dev
.. _Azure Pipelines: https://dev.azure.com/hdmf-dev/hdmf/_build
.. _README: https://github.com/hdmf-dev/hdmf#readme


--------
Coverage
--------

Code coverage is computed and reported using the coverage_ tool. There are two coverage-related badges in the README_
file. One shows the status of the `GitHub Action workflow`_ which runs the coverage_ tool and uploads the report to
codecov_, and the other badge shows the percentage coverage reported from codecov_. A detailed report can be found on
codecov_, which shows line by line which lines are covered by the tests.

.. _coverage: https://coverage.readthedocs.io
.. _GitHub Action workflow: https://github.com/hdmf-dev/hdmf/actions?query=workflow%3A%22Run+coverage%22
.. _codecov: https://codecov.io/gh/hdmf-dev/hdmf/tree/dev/src/hdmf

..  _software_process_requirement_specifications:


--------------------------
Requirement Specifications
--------------------------

There are 6 kinds of requirements specification in HDMF.

The first one is requirements-min.txt_, which lists the package dependencies and their minimum versions for
installing HDMF.

The second one is requirements.txt_, which lists the pinned (concrete) dependencies to reproduce
an entire development environment to use HDMF.

The third one is requirements-dev.txt_, which list the pinned (concrete) dependencies to reproduce
an entire development environment to use HDMF, run HDMF tests, check code style, compute coverage, and create test
environments.

The fourth one is requirements-opt.txt_, which lists the pinned (concrete) optional dependencies to use all
available features in HDMF.

The fifth one is requirements-doc.txt_, which lists the dependencies to generate the documentation for HDMF.
Both this file and `requirements.txt` are used by ReadTheDocs_ to initialize the local environment for Sphinx to run.

The final one is within setup.py_, which contains a list of package dependencies and their version ranges allowed for
running HDMF.

In order to check the status of the required packages, requires.io_ is used to create a badge on the project
README_. If all the required packages are up to date, a green badge appears.

If some of the packages are outdated, see :ref:`update_requirements_files`.

.. _requirements-min.txt: https://github.com/hdmf-dev/hdmf/blob/dev/requirements-min.txt
.. _setup.py: https://github.com/hdmf-dev/hdmf/blob/dev/setup.py
.. _requirements.txt: https://github.com/hdmf-dev/hdmf/blob/dev/requirements.txt
.. _requirements-dev.txt: https://github.com/hdmf-dev/hdmf/blob/dev/requirements-dev.txt
.. _requirements-opt.txt: https://github.com/hdmf-dev/hdmf/blob/dev/requirements-opt.txt
.. _requirements-doc.txt: https://github.com/hdmf-dev/hdmf/blob/dev/requirements-doc.txt
.. _ReadTheDocs: https://readthedocs.org/projects/hdmf/
.. _requires.io: https://requires.io/github/hdmf-dev/hdmf/requirements/?branch=dev


-------------------------
Versioning and Releasing
-------------------------

HDMF uses versioneer_ for versioning source and wheel distributions. Versioneer creates a semi-unique release
name for the wheels that are created. It requires a version control system (git in HDMF's case) to generate a release
name. After all the tests pass, CircleCI creates both a wheel (\*.whl) and source distribution (\*.tar.gz) for Python 3
and uploads them back to GitHub as a release_. Versioneer makes it possible to get the source distribution from GitHub
and create wheels directly without having to use a version control system because it hardcodes versions in the source
distribution.

It is important to note that GitHub automatically generates source code archives in .zip and .tar.gz formats and
attaches those files to all releases as an asset. These files currently do not contain the submodules within HDMF and
thus do not serve as a complete installation. For a complete source code archive, use the source distribution generated
by CircleCI, typically named `hdmf-{version}.tar.gz`.

.. _versioneer: https://github.com/warner/python-versioneer
.. _release: https://github.com/hdmf-dev/hdmf/releases
