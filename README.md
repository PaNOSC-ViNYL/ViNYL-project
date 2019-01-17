# ViNYL-project
This repository keeps track of tasks, milestones, deliverables of workpackage 5 in panosc [https://github.com/panosc-eu/panosc-eu.github.io].

## Schema of ViNYL and relation to other panosc workpackages
![](https://github.com/PaNOSC-ViNYL/ViNYL-project/blob/master/Workflow_CFGedits.png)

## Objectives 

    1. Expose existing instrument and experiment simulations capabilities as a virtual facility service in the EOSC to promote the access and integration of simulated data in complex analysis workflows.
    2. Build state-of-the-art e-infrastructures, providing a flexible simulation framework that enables users to rapidly implement simulation and analysis workflows specific to their facilities, instruments, and experiments.
    3. Make simulation data services inter-operable among themselves and with data analysis services and data catalogs through development of appropriate APIs and adoption of open data standards. 
    4. Enable RIs to seamlessly link the EOSC experiment simulation services to their in-house data reduction, analysis, and visualization infrastructures. Enable computational scientists to use the EOSC services and data catalogues (WP3) and analysis services (WP4) for validating their own bespoke structure or dynamics predictive modelling algorithms and to embed their tools in the EOSC.
    5. Foster the acceptance and adoption of open standards for data formats and APIs related to simulation services in the photon and neutron science community by developing simulation applications suitable for education and outreach and by simulating data sets for testing purposes of data tools and services. 
    
## Description of work 

Simulations of the various parts and processes involved in complex experiments play an increasingly important role in the entire lifecycle of scientific data generated at RIs: Starting with the idea for an experiment (often triggered by results from numerical and theoretical work), via design and optimization of experimental setups, estimation of experimental artifacts, generation of supporting material for beamtime proposals, assisting in decision making during an ongoing experiment to interpretation of experimental data, data analysis, and  finally extrapolation from the obtained results which then leads to new experiments. In particular, the analysis of experimental data often involves simulations e.g. to refine molecular or crystalline structures measured in diffraction experiments [[White2012](#references)].

Comparison between simulated and experimental data leads to insight not conceivable from experimental or simulated data alone: 
1. For the acquired raw data (on-line comparison with previously run simulations to assess and monitor data quality, enabling (automated or guided) optimization of  source, beamline, and instrumental configurations.
2. For the reduced data, as a sanity check for both experimental and simulated data.
3. For the results from the analysis step which had included all instrumental and experimental data and ended with a refined set of data for the particular sample.

Comparing reduced and analysed data is readily possible today, whereas it is not readily possible to compare raw data acquired from a real and a virtual experiment. Thus, algorithms to infer the likelihood that two sets of observations, one experimental and one theoretical, originate from the same underlying probability distribution need to be developed before it becomes possible to compare data without reducing them. Such algorithms would enable a direct validation of structural and dynamical sample (target) models and simulation techniques as they eliminate the dependency on the data reduction and analysis steps.

An objective of this work package is to facilitate the rapid prototyping and execution of  data workflows that combine experimental data and simulations inside user friendly application frameworks as an EOSC service. Ultimately, this will be achieved by creating a cloud based virtual research facility that represents all major components of real photon and neutron RIs and thereby allows the exchange and coupling of data and services between the real facility and its virtual simulated counterpart with the overarching objective to boost the extraction of meaning and information from raw experimental and simulation data.

The elements of the virtual facility are schematically shown in the block diagram figure 1. A virtual photon or neutron facility experiment consists of a sequence of simulations describing the physical and conceptual entities of the experiment. Starting from a simulation or model of the photon or neutron source followed by propagation of photons or neutrons through beamline and instrument optics to yield a precise characterization of the beam (temporal, spectral, and spatial structure, degree of coherence, divergence, and polarization)  and the very complex process of interaction of the beam with the sample (radiation damage) including the scattering of radiation and eventually the signal generation including a model or simulation of conversion of scattered intensity into a digital detector signal. Every process is simulated in a specific way. Often more than one implementation of a simulation algorithm and models of different levels of physical detail (e.g. ray tracing vs. wavefront propagation or atomistic first principle simulation vs. continuum models for radiation damage) exist. Establishing (where required) and maintaining (where already present)  interoperability and consistency of simulated data between these codes and modules as well as harmonization of APIs is a central task of this work package and key to the realization of the virtual facility. Careful design and documentation of our APIs will enable partner and non-partner RIs to plug-in their specific simulation softwares into the simulation chain and to create customized workflows for the specific virtual experiments needed in their facility. Finally, our APIs enable the integration of simulation capabilities and workflows including configuration and execution of simulation jobs, as well as retrieval, processing, and visualization of resulting simulation data in high level user interface frameworks such as jupyter-notebook [[Kluyver2016](#references)], Oasys [[Rebuffi2017](#references)], and others. This will be readily used in WP8 for expanding the usage of an existing e-learning platform.
APIs developed in the SIMEX workpackage in EUCALL [[Fortmann-Grote2017](#references)], the Atomic Simulation Environment (ASE [[Larsen2017](#references)]), and MDANSE [https://mdanse.org/] will serve as prototypes and seeds for our developments that focus on the creation of simulation and analysis data services in the EOSC.

## Tasks
For an up-to-date progress overview, go to the Projects page of this repository.

### Task 5.1 Simulation Infrastructure (M1-M48) Lead: XFEL.EU, Contributors: ESRF, ESS, CERIC-ERIC
Harmonization of simulation code APIs (SIMEX, ASE, WOFRY) and data formats to enable and to support interoperable simulations as  a cloud service. 
    • Harmonize APIs for beamline, sample trajectory, and signal generation simulation codes
    • Adopt simulation data formats: openPMD for particle and mesh data, NeXus for detector data (see WP3)

### Task 5.2 Photon and Neutron Source simulation data services (M1-M24) Lead: ESRF Contributors: XFEL.EU, ELI, CERIC-ERIC
Using the APIs from T5.1, expose photon source simulations as a cloud service for synchrotron and free-electron laser sources. Description, stockage and access to the parameters describing the source (storage ring Twiss parameters, insertion devices). Computation of the radiation. Decomposition of coherent modes with COMSYL [[Glass2017](#references)] and remote storage. Simulation of photons and neutrons from ultraintense laser-plasma interaction. Population of a radiation source database with precomputed beams containing intensity distributions and wavefronts.
    • Jupyter-notebook and execution environment (see WP4)
    • local OASYS workflows to access remote instrument description and data 
    • remote desktop session and execution environment (see WP4)

### Task 5.3 Photon and Neutron beamline simulation data services (M13-M36) Lead: ILL, CERIC-ERIC Contributors: ESRF, XFEL.EU, ELI
Expose photon and neutron beamline optics simulation services for photon and neutron facilities. Description of the beamline elements, deployment of scattering models for interaction of photon beams or wavefronts with optical elements (mirrors, crystals, lenses) and simulation data deposition in a database. Reuse existing libraries such as as SYNED, WOFRY, and support workflow-based high level user interface OASYS. Populate an instrument simulation database.
    • Jupyter-notebook and execution environment (see WP4)
    • local OASYS workflows to access remote instrument description and data
    • remote desktop session and execution environment (see WP4)

### Task 5.4 Simulation of signal generation including radiation-matter interaction  (M25-M48)  Lead: ESS, Contributors: ILL, XFEL.EU, ELI, CERIC-ERIC
Enable simulation of scattering signals from given sample structural dataset and beamline propagation data as a cloud service. 
Simulate interaction of radiation (from T5.2) with sample structural data stored e.g. in NOMAD as well as scattering and absorption signals.
    • Jupyter-notebook and execution environment
    • remote desktop session and execution environment
    • Protocol for comparison of raw simulated data vs. raw experimental data

### Task 5.5 Integrated simulation data workflows (M37-M48) Lead: XFEL.EU Contributors: ESRF, ILL, ESS, CERIC-ERIC 
    • Expose simulation data services in data analysis frameworks accessed via Jupyter notebooks or remote desktop solutions.
    • Iterative data analysis workflows including experiment simulations

## Deliverables
5.1 Prototype simulation data formats as openPMD domain specific extensions  including example datasets (M12, R, PU, XFEL.EU, ESS)

5.2 Release of documented simulation APIs (M24, O (Software), PU, XFEL.EU+ILL)

5.3 Repository of documented jupyter notebooks and Oasys canvases showcasing simulation
tasks executable via JupyterHub or remote desktop. (M42, O (Software), PU, XFEL.EU+ESRF)

5.4 VINYL software tested, documented, and released, including integration into interactive data analysis workflow with feedback loop. (M48, R+Software, PU, All)


## Milestones

| No. | Title               | WP| Due | Verification      |
|---------    	|------------------------------------------------       	|-------  	|-------   	|------------------------------------------------	|
|  			MS5.1 		     	|  			Simulation codes in PaNData 			Software Catalog 		        	|  			5 		     	|  			M6 		     	|  			PaNData software catalog 			website 		        	|
|  			MS5.2 		     	|  			Demonstration of simulation 			services 		        	|  			5 		     	|  			M24 		     	|  			Written report 		     	|
|  			MS5.3 		     	|  			VINYL software release 		     	|  			5 		     	|  			M42 		     	|  			Software released via open 			source repository 		        	|
|  			MS5.4 		     	|  			Validation of simulation 			services  			 		           	|  			4,5 		     	|  			M48 		     	|  			Written report 		     	|


## Resources

| Work package number 5 Lead beneficiary XFEL.EU  |  |  |  |  |  |  |
|---------    	        |---------------|-------  	|-------   	|--------	|  -----------|  -------------|
| Work package title VIrtual Neutron and x-raY Laboratory (VINYL) |
| Participant number             | 1 | 2 | 3 | 4 | 5 | 6|
| Short name of participant      | ESRF | ILL | XFEL.EU | ESS | ELI | CERIC-ERIC|
| Person months per participant: | 40 | 36 | 48 | 36 | 24 | 40|
| Start month 1 | End month 48|

## Risks

| Risk Description | Probability | WP involved | Proposed risk-mitigation measure |
|---------    	        |---------------|-------  	|-------  	|
| Data formats not published or not compatible with simulation data | Medium | 3,5 | Fall back on existing data formats (NeXus, CXIDB) and metadata standards (openPMD)|
| Developed APIs not compatible with data analysis framework | Medium | 4,5 | Monthly meeting with WP 4 contributors to address compatibility issues |
| Compute resources needed for testing and demonstrations not available or insufficient | High | 5 | Apply for HPC resources, e.g. PRACE preliminary access|

## References
[Fortmann-Grote2017] C. Fortmann-Grote et al. Simulations of ultrafast X-ray laser experiments Proc. SPIE, Advances in X-ray Free-Electron Lasers Instrumentation IV, International Society for Optics and Photonics, 2017, 10237, 102370S (2017). https://dx.doi.org/10.1117/12.2270552

[Glass2017] M. Glass, M. Sanchez del Rio  “Coherent modes of X-ray beams emitted by undulators in new storage rings”, Europhysics Letters, 119  3  (2017). https://dx.doi.org/10.1209/0295-5075/119/34004

[Jupyter2018], Project Jupyter, http://jupyter.org; formerly IPython. Accessed 15/3/2018 

[Kluyver2016] T. Kluyver. et al. Jupyter Notebooks – a publishing format for reproducible computational workflows IOS Press, 2016, 87 - 90 (2016). https://dx.doi.org/10.3233/978-1-61499-649-1-87

[Larsen2017] Ask Hjorth Larsen et al. The Atomic Simulation Environment—A Python library for working with atoms. J. Phys.: Condens. Matter Vol. 29 273002 (2017). https://dx.doi.org/10.1088/1361-648x/aa680e

[Maddison1997] Maddison, D. R.; Swofford, D. L. & Maddison, W. P. Cannatella, D. (Ed.) NeXus: An Extensible File Format for Systematic Information Systematic Biology, Oxford University Press (OUP), 1997, 46, 590-621 (1997) https://dx.doi.org/10.1093/sysbio/46.4.590

[Markvardsen2017] A. Markvardsen, “Report on Guidelines and Standards for Data Treatment software,” SINE2020 Deliverable 10.1 (2017) http://sine2020.eu/files/d10.1-guidelines-and-standards-1.pdf.

[Rebuffi2017] Rebuffi, L and Sanchez-del Rio, M., “OASYS (OrAnge SYnchrotron Suite): an open-source graphical environment for x-ray virtual experiments”, Proc. SPIE 10388, Advances in Computational Methods for X-Ray Optics IV, 103880S (2017). https://dx.doi.org/10.1117/12.2274263

[White2012] T. White etal. CrystFEL: a software suite for snapshot serial crystallography, Journal of Applied Crystallography, International Union of Crystallography (IUCr), 45, 335-341 (2012). https://dx.doi.org/10.1107/s002188981200231

