

Quick start
===========

Clone the repository::

  $ git clone git@repo.ctcc.no:dalton.git

In order to clone you need to upload your ssh key to https://repo.ctcc.no/my/account. To create an ssh key id_dsa.pub::

  $ cd .ssh
  $ ssh-keygen -t dsa
  
Build the code::

  $ cd dalton
  $ ./setup [--help]
  $ cd build
  $ make [-j4]

Run the test set::

  $ ctest [-j4]
