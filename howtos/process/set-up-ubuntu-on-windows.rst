.. _set_up_ubuntu_on_windows:

Set up Ubuntu on Windows for Sphinx development
###################################################

This guide will walk you through the process of installing and configuring
everything you need to be productive with git and Sphinx publishing using
OTC-TCS workflows. 

.. note::

   These instructions will only work on Windows build 16215 or later.

Install the Windows Subsystem for Linux
***************************************

#. Open a powershell terminal with administrative privileges and run the
   following command to enable the feature:

   .. code-block:: powershell

      Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

#. Open the Microsoft Store and search for Ubuntu. Select the latest version
   of Ubuntu distributed by the Canonical Group. As of the writing of this
   document, version 18.04 was the latest.  

   .. figure:: images/ms-store-ubuntu.png
      :width: 389px

   .. note::

      Do not attempt to use :command:`apt` to update to a newer version of Ubuntu within the Windows Subsystem for Linux envrionment. 

#. Install it.

   .. figure:: images/ms-store-ubuntu-get.png
      :width: 598px

#. After the installation has completed, launch the Ubuntu app from the 
   start menu. This launches an Ubuntu terminal window, which prompts you
   to create your user account.

Configure your Ubuntu distro for the proxy
******************************************

#. ~/.bashrc runs every time you log in to a terminal, so we need to add
   the following lines to the end of it:

   .. code-block:: bash

      export http_proxy=http://proxy-chain.intel.com:911
      export https_proxy=http://proxy-chain.intel.com:912
      export no_proxy=".intel.com,localhost"

#. APT is the package management software for Ubuntu. We need to create
   /etc/apt/apt.conf and add the following line to get it to work (this
   requires root privileges):

   .. code-block:: bash

      Acquire::http::Proxy "http://proxy-chain.intel.com:911";
      Acquire::https::Proxy "http://proxy-chain.intel.com:912";

#. SSH needs to know to use the proxy for github access, so we need to add
   the following lines to ~/.ssh/config:

   .. code-block:: bash

      host github.com
      port 22
      user git
      ProxyCommand nc -x proxy-us.intel.com:1080 %h %p

#. I needed to update permissions on the .ssh/config file:

   .. code-block:: bash

      chmod 600 ~/.ssh/config
      chown $USER ~/.ssh/config

Set up your ssh key
*******************

#. From the terminal run the following command, and use the default prompts
   (having a passphrase is recommended):

   .. code-block:: bash

      ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

   Output will reflect your environment but be similar to:

   .. code-block:: console

      Enter a file in which to save the key (/c/Users/you/.ssh/id_rsa):[Press enter]
      Enter passphrase (empty for no passphrase): [Type a passphrase]
      Enter same passphrase again: [Type passphrase again]

#. Now you'll need to copy the public key to github. Instructions for that
   are here: https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/

Install dependencies
********************

#. We need to get APT up to date before we start adding software
   packages:

   .. code-block:: bash

      sudo apt update

#. Some packages that might be useful for documentation:

   .. code-block:: bash

      sudo apt install doxygen graphviz default-jre

#. Python3 should be installed, so now we just need to install pip:

   .. code-block:: bash

      sudo apt -y install python3-pip

#. Create a file called requirements.txt and add the following:

   .. code-block:: bash

      breathe==4.9.1
      sphinx==1.7.5
      docutils==0.14
      sphinx_rtd_theme
      sphinxcontrib-plantuml

#. Run the following command from the terminal to install the above Python
   modules for Sphinx development:

   .. code-block:: bash

      pip3 install -r requirements.txt


Some Rules
**********

#. If you want to use a Windows GUI editor (Sublime, for example), then
   files must be stored on the Windows partition. Files located on your
   Windows filesystem can be found from the Linux partition here:

   .. code-block:: bash

      /mnt/c/rest/of/path

   A downside to this is that paths become quite long. You can workaround
   this by creating a symlink in your Ubuntu home directory: 

   .. code-block:: bash

      ln -s /mnt/c/path/to/your/git_repos ~/work_dir

   And it can be used like this:

   .. code-block:: bash

      cd work_dir

   .. note:: 

      This is important, because you must never edit files in the Linux
      partition from Windows: https://blogs.msdn.microsoft.com/commandline/2016/11/17/do-not-change-linux-files-using-windows-apps-and-tools/