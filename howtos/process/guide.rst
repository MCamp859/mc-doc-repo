.. _guide:

Documentation Template Setup Guide
##################################

This guide teaches you how to setup, configure, and publish this site
as a template for your own Intel sponsored open-source documentation
project. 

Overview
========

This project workflow is designed to make publishing and managing community
contributions as easy as possible. Documents are written in reStrucutredText
and published as a static website with `Sphinx <http://www.sphinx-doc.org>`_
. `GitHub <http://github.com>`_ hosts both the source repository and the
documentation website. 

Publishing this template for your open-source project works best on a Linux\*
based operating system, though it can be done from Windows\* with some
additional effort. At a minimum, you will need a basic knowledge of Git
and the bash command line. You can find an introduction to Git and the
GitHub workflow in our :ref:`doc_gen`.

This guide assumes that you have already received approval for your
open-source project and that your Intel sponsored GitHub project exists. If
not, please see the prework below.

Prework
-------

* Open-source approval process: 
  https://opensource.intel.com/how-to/open-source-approval-process 

* Open-source whitelist process: 
  https://opensource.intel.com/how-to/open-source-whitelist-process

* Open-source development model:
  https://opensource.intel.com/how-to/open-source-intel-open-source-development-model

* Request a GitHub project under Intel sponsorship:
  https://opensource.intel.com/how-to/otc-infrastructure/github

Setup the Documentation Source Repository (doc-repo)
====================================================

#. Create a new repository on GitHub.com by clicking the new button from the
   project repositories tab.

   .. figure:: images/new-git-repository.png
      :width: 815px

#. Name your repository ``doc-repo`` and click ``create repository``.

   .. figure:: images/name-git-repo.png
      :width: 665px

Populate Documentation Source Repository
========================================

The source documents for this website are hosted on Intel's Enterprise GitHub
site. Rather than start from scratch, we can use the source to bootstrap
your documentation project.

.. note:: 

   This process, like creating the new repository on GitHub, need only be
   performed once per project. Once the template source repository is set
   up, new contributors need only fork the existing source repository. 

#. Create a working directory for publishing your documentation. For this
   example, we'll call it ``otc-tcs-test``.

#. Retrieve the document template source as a zip file from the 
   `OTC TCS repository <https://github.intel.com/otc-tcs/documentation-template>`_.

   .. figure:: images/get-git-zip.png
      :width: 325px

#. Move the .zip file to the working directory -- ``otc-tcs-test``. 

   .. code-block:: console

      user@yourcomputer:~/otc-tcs-test$ ls -al
      total 6684
      drwxrwxrwx 0 root root     512 Jul 27 13:02 .
      drwxrwxrwx 0 root root     512 Jul 27 12:48 ..
      -rwxrwxrwx 1 root root 6843594 Jul 27 12:46 documentation-template-master.zip

#. Unzip the document template, rename it ``doc-repo``, and remove the .zip
   archive.

   .. code-block:: console

      user@yourcomputer:~/otc-tcs-test$ unzip documentation-template-master.zip # unzip the archive
      user@yourcomputer:~/otc-tcs-test$ mv documentation-template-master doc-repo # rename the directory
      user@yourcomputer:~/otc-tcs-test$ rm documentation-template-master.zip # remove the archive

   The contents of your ``otc-tcs-test`` directory should look like this:

   .. code-block:: console

      user@yourcomputer:~/work_dir/otc-tcs-test$ ls -al
      total 0
      drwxrwxrwx 0 root root 512 Jul 27 14:35 .
      drwxrwxrwx 0 root root 512 Jul 27 12:48 ..
      drwxrwxrwx 0 root root 512 Jul 19 10:44 doc-repo

#. Initialize ``otc-tcs-test/doc-repo`` as a Git repository and add all 
   the files in the ``doc-repo`` directory. 

   .. code-block:: console
      
      user@yourcomputer:~/otc-tcs-test$ cd doc-repo # these commands must be run from within the doc-repo directory
      user@yourcomputer:~/otc-tcs-test/doc-repo$ git init # initialize the directory as a repository
      user@yourcomputer:~/otc-tcs-test/doc-repo$ git add . # stage all files
      user@yourcomputer:~/otc-tcs-test/doc-repo$ git commit -m "First Commit" # commit them to the repository and add a message 

#. Copy GitHub URL of GitHub Documentation Source Repository by clicking the
   clipboard button. The following UI only appears if the repository is
   empty. 

   .. figure:: images/get-git-url.png
      :width: 773px

#. Set up remote link between local ``doc-repo`` and GitHub Documentation
   Source Repository

   .. code-block:: console

      user@yourcomputer:~/otc-tcs-test/doc-repo$ git remote add origin git@github.com:yourproject/doc-repo.git

#. Push the contents of ``otc-tcs-test/doc-repo`` to the GitHub Documentation
   Source Respository. 

   .. code-block:: console

      user@yourcomputer:~/otc-tcs-test/doc-repo$ git push origin master

#. Verify that your push was successful by checking the contents of the 
   ``<> Code`` tab for the ``doc-repo`` repository.

   .. figure:: images/check-repo.png
      :width: 786px

You are now ready to set up your :ref:`publication respository <template_publish>`.