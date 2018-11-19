
Unix Tutorial
=============

This is a unix tutorial intented for scientist with little or no unix experience.

**Contributors**:

- Benoist LAURENT (main developper)
- Ingrid LAFONTAINE


Run a local Jekyll server
-------------------------

.. code-block:: bash

    cd docs
    eval "$(~/.rbenv/bin/rbenv init -)"
    rbenv global 2.5.1
    bundle exec jekyll serve -w
