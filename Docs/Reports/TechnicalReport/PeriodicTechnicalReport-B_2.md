
# Table of Contents

1.  [1.2.5 Work package 5 - Virtual Neutron and X-ray Laboratory (VINYL)](#orgdea7bdc)
    1.  [Task T5.1 Simulation infrastructure](#org8024195)
    2.  [Task T5.2 Photon and Neutron Source simulation data services](#orgb713565)
    3.  [Task T5.3 Photon and Neutron beamline simulation data services](#orgcc50d5e)
    4.  [Task 5.4 Simulation of signal generation including radiation-matter interaction](#orgb799e4a)
    5.  [Future work](#org4108064)


<a id="orgdea7bdc"></a>

# 1.2.5 Work package 5 - Virtual Neutron and X-ray Laboratory (VINYL)

Activities in work package 5 ("Virtual Neutron and x-raY Laboratory - VINYL)
were distributed across all Tasks except for T5.5. We report on each task below:


<a id="org8024195"></a>

## Task T5.1 Simulation infrastructure

The central aspect of Task 5.1 is the development of a harmonized simulation API
and it's adoption in the three simulation frameworks (*SIMEX*, *Oasys* and
*McStasScript*). Through coordinated efforts across all RIs, including a two
week development sprint in September 2020, the python library *libpyvinyl*
([https://github.com/PaNOSC-ViNYL/ViNYL-project/libpyvinyl](https://github.com/PaNOSC-ViNYL/ViNYL-project/libpyvinyl)) has matured to a
point where first successfull adoptions in *McStasScript* have been demonstrated.
Further adoption in *SIMEX* and *Oasys* was challenging due to a missing class
representing simulation data in *libpyvinyl*. This class has hence been added to
the library and adoption in *SIMEX* and *Oasys* (in particular the raytracing engine
*Shadow3*) can now take place. The Parameters class in *libpyvinyl* builds on the
instrument database (see Task 5.3) to query parameters and permissive values or
ranges. All RIs contributed via to the
specification, implementation, testing, review, and adoption of *libpyvinyl*. A
second major activity in T5.1 was the dissemination of openPMD standard
extensions in the community. After submission in fulfillment of Deliverable
D5.1, the standard extensions were reviewed by the openPMD maintainers. In the
meantime, two extensions (Molecular Dynamics and Wavefronts, both led by EuXFEL)
have been merged into the mainline repository and will be part of the openPMD
version 2 release. Another extension (Raytracing, led by CERIC-ERIC, ESS, and
ILL) is currently under review after it had undergone substantial changes
requiremed by the instrument database (see Task 5.3). Our raytracing extension
will most likely remain a standalone standard because of conflicting design
choices in the openPMD mainline extension for beam data (Beamphysics extension).


<a id="orgb713565"></a>

## Task T5.2 Photon and Neutron Source simulation data services

In Task 5.2, the code *COMSYL* for simulation of partially coherent x-ray sources
and propagation has been made accessible as a web service (work led by ESRF).

The x-ray pulses simulation database for coherent x-ray source simulations at
Eu.XFEL and can now be accessed from the *SIMEX* photon experiment simulation
library (work led by Eu.XFEL). *Oasys* workspaces describing ESRF beamlines are
exposed to *Oasys* users through a dedicated github repository (see also Task
5.3).


<a id="orgcc50d5e"></a>

## Task T5.3 Photon and Neutron beamline simulation data services

The idea of our
beamline simulation services is to give users a starting point for simulations
of photon or neutron beams propagating from the source to the experimental
endstation in *Oasys*, *McStasScript*, or *SIMEX*.

For *Oasys* (development led at ESRF and CERIC-ERIC), a github repository has
been created at [https://github.com/PaNOSC-ViNYL/Oasys-PaNOSC-Workspaces](https://github.com/PaNOSC-ViNYL/Oasys-PaNOSC-Workspaces) that
contains a collection of *Oasys* workspaces (binary data files that define a
workflow in *Oasys* including optical beamline elements, their order and
orientation and beam parameters). These workspaces model various beamlines at
the ESRF. More beamlines for ESRF and for other photon RIs will be added
shortly, in preparation for the Deliverable 5.3. From within *Oasys*, the
repository can be browsed similar to a local file directory and the user can
select a workspace for download and open it in *Oasys*. The user can then
adjust the beamline parameters to her needs.

In a similar way, *McStasScript* provides preconfigured setups representing
neutron beamlines at ESS. These can be imported into the simulation environment
e.g. in a *jupyter notebook*.

For *SIMEX*, the github
repository [https://github.com/PaNOSC-ViNYL/wavefrontDB](https://github.com/PaNOSC-ViNYL/wavefrontDB) fulfills this role of a
beamline repository. Through the python library *WPG* (WavePropaGator), it is furthermore possible
to load beamline definitions from the online beamline simulation tool *SiREPO*
([https://www.sirepo.com/srw#](https://www.sirepo.com/srw#)).

The beamline parameters themselves are maintained in a json file collection
which is parsed by *libpyvinyl* to infer beamline parameters and permissive
values and ranges.


<a id="orgb799e4a"></a>

## Task 5.4 Simulation of signal generation including radiation-matter interaction

As a first measure in Task 5.4, we have drafted a protocol for the comparison of
raw simulated to raw experimental data. The final version will be released with
Deliverable 5.4 together with a working example of a benchmark comparison.

At EuXFEL, work is continuing to ease integration of radiation-matter interaction
codes in SIMEX.

Building on *McStasScript*, a prototype for integration of beamline and signal
simulations in the data aquisition and control system at ILL has been developed.
It allows the seemless switching between experimental data and simulated data on the control screen
which is a useful feature for beamline tuning and signal estimation tasks.

At ELI, several use cases have been developed that make use of the new
capabilities to connect various simulation codes. E.g. use case 18 connects McStas
Simulations of neutron beams with DFT target simulations to study the defect
location dependent diffraction signals from Boro-carbon systems.


<a id="org4108064"></a>

## Future work

Beyond these tasks, initial work has been undertaken to prepare the deployment
of our simulations as web services. To this end, docker containers have been
created for *Oasys*, *McStas-McStasScript*, and *SIMEX* which can be launched e.g. in
a jupyterhub environment. These containers are being used in the integration of
simulations in the e-learning platform "pan-learning" developed in work
package 8. The containers and the recipes how to build the containers now form the basis
for work in Task 5.5.

Our simulation API library *libpyvinyl* has been improved during another
development sprint in Dec. 2021 (outside the reporting period) and will be
released in Q1 2022 on the python package index (pypi). This will then enable
the stable adoption of *libpyvinyl* in further simulation frameworks, stabilized
build recipes for simulation docker containers and deployment of simulation web
services. In parallel, the instrument database and simulation data repositories
mentioned above will be enriched with more data to represent a larger variety of
RI beamlines, instruments, and experimental conditions.

