

How you can contribute to this documentation
============================================

These pages are rendered using `RST/Sphinx <http://sphinx-doc.org/rest.html>`_ and served using
`Read the Docs <https://readthedocs.org>`_.
RST is a subset of Sphinx. Sphinx is RST with some extensions.


How to modify the webpages
--------------------------

The source code for this documentation is hosted on `GitHub <https://github.com/daltonprogram/devguide>`_.
You need a `GitHub <https://github.com>`_ account to modify the sources.

With a GitHub account you have two possibilities to edit the sources:

* You write an email to bast at kth dot se and ask to be added as project team member. After that you can push
  directly to https://github.com/daltonprogram/devguide. Once you commit and push, a webhook
  updates the documentation on http://dalton-devguide.readthedocs.org/. This typically takes less than a minute.
* You fork https://github.com/daltonprogram/devguide and submit your changes at some point via a pull request. This means
  that your changes are not immediately visible but become so after a team member reviews your changes
  with a mouse click thus integrating them to https://github.com/daltonprogram/devguide.


How to locally test changes
---------------------------

You do not have to push to see and test your changes.
You can test them locally.
For this install python-sphinx and python-matplotlib.
Then build the pages with::

  make html

Then point your browser to _build/html/index.html.
The style is not the same but the content is what you
would see after the git push.
