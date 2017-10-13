Setup Instructions
*****************************

To get flow\_dev running, you need three things: flow\_dev (or
flow), SUMO, and rllab. Once each component is installed successfully,
you might get some missing module bugs from python. Just install the
missing module using your OS-specific package manager / installation
tool. Follow the shell commands below to get started.

Installing Flow
=================

Create a conda environment (add warning, that EVERYTHING is a specific version):
:: 

    conda create -n flow python=3.5.2
    source activate flow

Install rllab-multiagent (NOTE TO TEAM: For now, it's still rllab-distributed)
::

    git clone git@github.com:cathywu/rllab-multiagent.git
    cd rllab-multiagent
    git checkout flow_release  # TODO eliminate this step

For OSX
::

    brew install swig sdl sdl_image sdl_mixer sdl_ttf portmidi

For Linux
::

    sudo apt-get install swig
    sudo apt-get build-dep python-pygame
    sudo apt-get build-dep python-scipy

::

    python setup.py develop

Install flow within the rllab-multiagent repo
::

    git clone https://github.com/cathywu/flow.git  # Needs to be here for AWS experiments using rllab  (NOTE TO TEAM: This eliminates the make prepare step.)
    cd flow 
    ./scripts/setup_sumo_osx.sh <DESIRED_PATH_TO_SUMO> # installs sumo
    python setup.py develop  # (install flow, rllab, and dependencies)
    cp flow/core/config.template.py flow/core/config.py  # TODO eliminate or move to setup_osx.sh or add to commonly asked questions

Test the installation
=====================

Running the following should result in the loading of the SUMO GUI.
Click the run button and you should see unstable traffic form after a
few seconds, a la (Sugiyama et al, 2008).

Run the unit tests:

::

    nose2

Let’s see some traffic action:

::

    python examples/sugiyama.py

This means that you have Flow properly configured with SUMO.

::

    python examples/mixed-rl-single-lane.py

This means that you have Flow properly configured with both SUMO and
rllab. Congratulations, you now have Flow set up!