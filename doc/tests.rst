

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


Nightly testing dashboard
=========================

We have two testing dashboards, https://repo.theochem.kth.se/cdash/?project=DALTON, and
https://repo.theochem.kth.se/cdash/?project=LSDALTON.

This is the place to inspect tests which are known to fail (ideally none).

By default CTest will report to https://repo.theochem.kth.se/cdash/?project=DALTON. You
can change this by setting ``CTEST_PROJECT_NAME`` to "LSDALTON" (or some other dashboard)::

  $ export CTEST_PROJECT_NAME=LSDALTON

By default the build name that appears on the dashboard is set to::

  "${CMAKE_SYSTEM_NAME}-${CMAKE_HOST_SYSTEM_PROCESSOR}-${CMAKE_Fortran_COMPILER_ID}-${BLAS_TYPE}-${CMAKE_BUILD_TYPE}"

If you don't like it you can either change the default, or set the build name
explicitly::

  $ ./setup -D BUILDNAME='a-better-build-name'

Then run CTest with -D Nightly or Experimental::

  $ ctest -D Nightly      [-jN] [-L ...] [-R ...]
  $ ctest -D Experimental [-jN] [-L ...] [-R ...]

If you want to test your current code, take Experimental. If you want to set
up a cron script to run tests every night, take Nightly.

Currently the above recipes for Nightly/Experimental will compile all targets.
If you want to compile only LSDALTON within Nightly/Experimental, you can do this::

  $ make lsdalton.x
  $ ctest -L linsca -D NightlyTest
  $ ctest -L linsca -D NightlySubmit

This does not report configure/build problems. We will streamline this soon.

If you have an iPhone you may find this useful:
http://repo.theochem.kth.se/cdash/iphone/project.php?project=DALTON
