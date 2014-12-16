

Running tests
=============

We currently have two to four coexisting
test mechanisms:

- Traditional shell script tests using ``TEST`` scripts; these are being phased out
- Perl scripts; these are being phased out
- Runtest based scripts, see: http://runtest.readthedocs.org
- CTest

CTest wraps around runtest. Runtest is for
individual tests. CTest ties them all together and produces a test runner.  The
preferred way to run tests is through CTest inside the build directory.

You can run all tests::

  $ ctest

all tests in parallel::

  $ ctest -jN

You can match test names::

  $ ctest -R somename

or labels::

  $ ctest -L essential

to see all options, type::

  $ man ctest

To see all labels, browse ``cmake/Tests(LS)DALTON.cmake``.

You can also run tests individually, for this execute the individual python
``test`` scripts and point it to the correct build directory (try ``./test -h``
to see all options).

FIXME: We should here describe what tests we require to pass before pushing
anything to master.


Writing tests
=============

Have a look here: http://runtest.readthedocs.org

And have a look at other test scripts for inspiration.  You have there full
python freedom. The important part is the return code. Zero means success,
non-zero means failure.

To make a new test you have to make a folder, which is the test name, and put a
mol and a dal file in that folder. You also have to include a reference output
in a sub-folder "result/".  Then you can just copy a "test" file from one of the
other test directories and modify it according to your needs (there is no for
this).

You have to add your new test to
``cmake/Tests(LS)DALTON.cmake``. Then do::

  $ cmake ..

in your build directory. Finally you can run your new test with the command::

  $ ctest -R my_new_test

Your test folder will not be cluttered with output files if you are running the
test from the build directory.

You can also adjust the test and execute it directly in the test directory but
then be careful to not commit generated files.
