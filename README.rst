Ploneintranet Jenkins configuration
===================================

The Ploneintranet contains a lot of code and has a good code coverage.
To make testing faster and easier, we use a jobbuilder to generate the jobs.
We aim to have quicktests that test only parts of the code and that should give fast feedback, we want to have superclean tests that test everything and don't mask errors because we build everything in a place that has been used before. And for good measurement, we want to have a relativly clean complete test run that is not so slow.

With the help of `Jenkins Job Builder <http://ci.openstack.org/jenkins-job-builder/index.html>`_ from openstack we manage to do this without getting mad. At the time of writing, we create 33 Job configurations.

Installation of configuration tool
----------------------------------
We use the Jenkins Job Builder with extensions provided by Gil Forcada. If you want to run this configuration, you must use his fork, because the Xvfb extension is not yet in upstream. Check the source out from `https://github.com/gforcada/jenkins-job-builder.git`.

There is no package, so you simply create a virtualenv and install or develop the source checkout directly via ``python setup.py develop``

After this, you must provide your credentials. You can copy the ``jenkins_jobs.ini_tmpl`` and adapt it to your needs. You only need to add your username andd password. ``jenkins_jobs.ini`` has been added to ``.gitignore``, so you will have a hard time to accidentally commit your credentials.

Changing the configuration
--------------------------
The script so far only looks for the configuration file in ``/etc/someting``. We do not promote this behavior and suggest to always declare your configuration file explicit.

The tool contains a small set of commands. The most common one, to upgrade projects, works like this::

    jenkins-jobs --conf jenkins_jobs.ini update jobs.yml
