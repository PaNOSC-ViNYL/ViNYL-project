# Specifications for Simulation APIs in ViNYL

Simulation APIs in ViNYL serve the following purposes:

* Provide a harmonized user interface to simulation codes (aka "backengine")
  for various photon and neutron simulation tasks.
* Every backengine is represented by one and only one (specialized) API ("Calculator")
* Specialized Calculators that represent the same or similar physics (e.g.
  photon beam transport, scattering, detectors) derive from a common
  ancestor, an Abstract Calculator.
* All Abstract Calculator derive from the Abstract Base Calculator (ABCalc).
* The basic user interface is defined on the level of the ABCalc:
    * Instantiation:

    ```
    some_calculator = CalculatorName(parameters=parameters, inpath="/path/to/input/data", outpath="/path/to/output/data")
    ```

    * Copy construction:

    ```
    new_calculator = old_calculator(parameters=new_parameters, inpath="/new/inpath", outpath="/new/outpath")
    ```

    * Dump a calculator (Save object as a binary file, similar to `pickle`)

    ```
    calculator.dump(fname="dumpfile.dill")
    ```

    The dump method is to be implemented using the `dill` library.

    * Resurrect a calculator from a dumpfile:

    ```
    calculator = Calculator(dumpfile)
    ```




