camlistore Google Compute Image packer config
===========================================

This is a packer configuration for building a Google Compute Image with
camlistore preinstalled.

To use it, you must first install `Packer <https://packer.io/>`.

Create a file called ``vars.json`` that contains something like this, using
actual values from your own Google Cloud account:

.. code-block:: javascript

    {
        "google_account_file": "account.json",
        "google_project_name": "foo-bar-baz-123"
    }

Once you've got all this in place you can then run packer::

    packer build -var-file=vars.json camlistore-server.json

If it runs successfully to completion then you will get the id of an image that
has the camlistore binaries in ``/usr/local/bin`` and the necessary files for
the web UI in ``/usr/local/lib/camlistore``. A system user is also created,
called ``camlistore``, which should be used to run camlistore in preference
to ``admin``, since Camlistore does not deserve nor want access to run
``sudo``.

Once you've booted the created image you'll need to create a server config
in ``/home/camlistore/.config/camlistore/server-config.json``.
You can then run ``camlistored`` (as the user ``camlistore``) to start up the
Camlistore server using that configuration.

Have fun!
