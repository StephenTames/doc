.. index::
  pair: Developer, Dev Mode

.. _dev_guide_dev_env:

Dev Environment
---------------

Our development environments include a *working* administrative server
for testing. It is very important in our process that developers are
able to run deployments in their environment as part of the testing
cycle.

> Protip: You can enter the Rails Console from the host, using ``docker exec -it compose_rebar_api_1 /opt/digitalrebar/core/tools/rails-console.sh``.


.. toctree::
  :maxdepth: 1
  :glob:

  *

Docker Cheats for Developers
----------------------------
.. _dev_guide_docker:


While you can always use `docker exec -it compose_rebar_api_1 bash` to get into the API container, here are some handy cheats that you can use to do routine tasks inside the API container:

* Tail Logs: ``docker exec -it compose_rebar_api_1 tail -f /var/log/rebar/production.log``
* Open Rails Console (to test models & database direct): ``docker exec -it compose_rebar_api_1 /opt/digitalrebar/core/bin/rebar_console``
* Use the CLI: ``docker exec -it compose_rebar_api_1 rebar ping``
* Reimport Barclamps: ``docker exec -it compose_rebar_api_1 /opt/digitalrebar/core/bin/barclamp_import opt/digitalrebar/[workload]/rebar.yml``


Setting Rails Development Mode
------------------------------

.. _dev_guide_dev_mode:

Digital Rebar does not use use RAILS_ENV=development in the traditional way because most of our testing is targeted at doing real provisioning work that requires the production system.

If you have a need for development behavior (classes and views the refresh when code changes) then perform the following steps:

#. Deploy Digital Rebar in the normal way
#. From the host, create the ``dev.mode`` file in the digitalrebar home directory and restart the rebar_api contain

   ```touch ~/digitalrebar/dev.mode
   cd ~/digitalrebar/deploy/compose && docker-compose restart rebar_api
   ```

You may make any Rails configuration changes by created your own ``core/rails/config/environments/production.rb`` file.  Since we git ignore ``production.rb`` you can leave your own customized version in place.
