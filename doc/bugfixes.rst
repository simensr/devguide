

Reporting and fixing bugs
=========================


Where to report bugs
--------------------

We track issues at https://repo.ctcc.no/projects/dalton/issues.
Please report and discuss bugs there.

In addition you can discuss serious bugs in the developers section of the
`Dalton forum <http://daltonprogram.org/forum>`_.


How to commit a bugfix
----------------------

**Before you commit a bugfix think very carefully to which branch you commit the bugfix to.**

At the time of writing we have 3 longer lived branches
(next to many feature branches)::

  Dalton2014                   ---------->
                              /
  master           ---------------------->
                      \
  Dalton2013_release   ------------------>

Dalton2013_release is the branch supporting Dalton 2013 and its patches,
Dalton2014 is the branch supporting Dalton 2014 and its patches,
master is the main development branch.
Dalton2013_release lives until Dalton 2014 is released.

We never merge master to release branches. This means that bugfixes
committed to master after the release branch has been created
never make it into a Dalton 2013 or 2014 release or patch (see cross)::

  Dalton2014                   ---------->
                              /
  master           --------------x------->
                      \
  Dalton2013_release   ------------------>

This is fine for code changes which are irrelevant for the
released or soon to be released version.

However, patches and bugfixes which are relevant for the released or soon to be released
versions need to be committed to the respective release branch and merged
to master::

  Dalton2014                   -----x---->
                              /      \
  master           ---------------------->
                      \         /
  Dalton2013_release   --------x--------->

We can summarize that all commits that go a release branch will be integrated
to the master branch but not the other way.  If you are not sure where to
commit to, better ask the forum.  If you committed to the wrong branch by
accident, then ask for help. Do not transfer commits manually.

Checklist for commits to a release branch supporting an already released version:

* Never push unfinished work to the release branch.
  This is because at any moment we can create a patch and we do not want to release patches with unfinished work.
  The person who releases the patch cannot know that you meant to push something else soon to complete your work. Commit locally as often as you want but push finished units.
* Test the bugfix/change as good as you can before pushing to the release branch.
  Make sure that you don't break other functionality with your bugfix.
* Describe the change in the file CHANGELOG.rst.
  The person who creates and publishes the patch will not browse logs or remember your commit log message;
  the person creating the patch will only look into CHANGELOG.rst to inform users about changes.
* Do not bump VERSION. This is because we will typically collect few fixes into one patch; the person who publishes the patch will do it.
* After you are done, merge your change to master so that people on the master branch benefit from your change.
* If the merge to master conflicts, then don't leave it like that. Either resolve the conflict or ask for help if you cannot do it.
  The longer we wait the more conflicts we will have.
* If this is a critical bugfix, inform other developers so that they know about it and that the patch gets published ASAP.
