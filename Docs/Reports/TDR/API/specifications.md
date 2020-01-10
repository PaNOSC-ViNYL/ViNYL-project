# Specifications for Simulation APIs in ViNYL


Simulation APIs in ViNYL provide a harmonized user interface to simulation codes (aka "backengine")
for various photon and neutron simulation tasks. The API is split into
`Calculators` and `Parameters`. To every `Calculator` corresponds one
`Parameters` class. `Parameters` are shallow objects (state engines) that
encapsulate the physical and numerical parameters needed to setup a
simulation. `Calculators` wrap their respective `backengine`, and manage
input/output tasks.

## Calculators
### Specifications
* Every `backengine` is represented by one and only one (specialized) `Calculator`.
* Different specialized `Calculators` that represent the same or similar physics (e.g.
  photon beam transport, scattering, detectors) derive from a common
  ancestor, an `AbstractCalculator`.
* All `AbstractCalculator`s derive from the `AbstractBaseCalculator` (`ABCalc`).
* The basic user interface is defined on the level of the `ABCalc`:
    * Instantiation:

    ```
    calculator = CalculatorName(parameters=parameters, inpath="/path/to/input/data", outpath="/path/to/output/data")
    ```

    * Copy construction:

    ```
    new_calculator = old_calculator(parameters=new_parameters, inpath="/new/inpath", outpath="/new/outpath")
    ```

    * Dump a calculator (Save object as a binary file, similar to `pickle`)

    ```
    calculator.dump(filename=...)
    ```
    The dump method is to be implemented using the `dill` library.

    * Resurrect a calculator from a dumpfile:

    ```
    calculator = Calculator(filename=...)
    ```

    * Run a simulation

    ```
    calculator.run()
    ```

    * Query the simulation data

    ```
    data = calculator.data
    ```

    * Write simulation data to disk.

    ```
    calculator.saveH5(openpmd=True)
    ```
    The `openpmd` flag (`bool`) instructs to write output to openpmd compliant `hdf5` file using
the `openpmd-api` and applying the openpmd domain extensions developed in
Deliverable D5.1. It's value is `True` by default.

## Parameters
Simulation parameters (**not** input data) are encapsulated in a `CalculatorParameters`
object. `CalculatorParameters` classes are organized in a similar hierarchy as `Calculators`
with an `AbstractCalculatorParameters` class at the top, domain specific
`DomainCalculatorParameters` in the middle layer, and
`SpecializedCalculatorParameters` at the bottom.

`CalculatorParameters` are state engines. They contain the parameter values and
"know" about the inner logic of these parameters such that consistency checks
can be performed, but they do not carry out any kind of simulation.

### Specifications:

* Construction:

```
parameters = CalculatorParameters(param1=value1*unit1, param2=value2*unit2, ...)
```
Individual parameters shall be given physical units. Units are derived from
the `pint` module.

* Copy construction:

```
new_parameters = old_parameters(params1 = new_value, ...)
```

* Serialize parameters

```
parameters.serialize(filename=)
```
The dump() method shall write the parameters to a `json` formatted file. Use the
`json` package.

* De-serialize (construct from serialization):

```
parameters = CalculatorParameters("filename.json")
```

* Member attributes:
Individual parameters are member attributes of the `CalculatorParameters` class.
Access to these attributes shall be organized as `properties`. Example:

```
class WavePropagatorParameters(PhotonBeamTransportParameters):

    def __init__(self, beamline=spb_beamline, ...)
        """
        Constructor for the WavePropagatorParameters object.

        :param beamline: The beamline through which to propagate the beam.
        :type  beamline: WPG.Beamline

        :param ...: ...
        :type  ...: ...

        ...

        """

        self.beamline = beamline
        ...


    @property
    def beamline(self):
        """ Set/get the beamline of the propagation """

        return self.__beamline

    @beamline.setter
    def beamline(self, value):

        # Perform checks:
        if not isinstance(value, WPG.Beamline):
            raise TypeError("Wrong type for parameter 'beamline'. Expected {},
received {}.".format("WPG.Beamline", type(val)))

        ... # more checks.

        self.__beamline = val

```












