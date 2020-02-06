# McStasScript integration into harmonized API

Assuming the form of parameters and calculators:

```
calculator = CalculatorName(parameters=parameters, inpath="/path/to/input/data", outpath="/path/to/output/data")
parameters = CalculatorParameters(param1=value1*unit1, param2=value2*unit2, ...)
```

Could take an McStasScript instrument object as “parameters”, inpath rarely necessary, could dump data in outpath. Would violate design principles on parameters, as the parameter object would contain methods
for performing the simulation.

```
# my parameters is McStasScript instrument object
my_parameters = McStasScript(name=“ODIN”, author=“Mads”)
 
# Now that my_parameters is an instrument object, information can slowly
be added
src = my_parameters.add_component(“source”, “source_simple”)
src.xwidth = 0.1
src.yheight = 0.1
src.E0 = 10
src.dE = 2
 
my_parameters.add_parameter(“theta”, value=10)
 
mono = my_parameters.add_component(“mono”, “Monochromator_flat”)
mono.xwidth = 0.03
mono.yheight = 0.05
mono.Q = 1.22
mono.set_AT([0, 0, 1], RELATIVE=“source”)
mono.set_ROTATED([0, “theta”, 0], RELATIVE=“source”)
 
my_parameters.add_declare_var(“two_theta”)
my_parameters.append_initialize(“two_theta = 2.0*theta;”)
 
beam_dir = my_parameters.add_component(“beam_dir”, “Arm”)
beam_dir.set_AT([0,0,0], RELATIVE=“mono”)
beam_dir.set_ROTATED([0,”two_theta”,0], RELATIVE=“source”)
 
# Could have necessary datafiles and similar in inpath
# Results written to outpath
my_calculator = McStas(parameters=my_parameters, inpath=“/path/to/input/data”, outpath=“/path/to/output/data”)
 
my_calculator.run()
 
data = my_calculator.data
```

Calculator could also be used to instantiate an instrument object, the only
problem is that it does not make much sense to insert parameters
immediately. Would need to insert parameters in run call. Also since
most information is passed after the creation of the instrument object,
there is very little information in the associated parameter class.
Internal checking is however done whenever information is added to the
instrument object regardless, so the input sanitation duty is being
performed somewhere.

```
# my parameters is small and almost trivel
my_parameters = McStasParameters(name=“ODIN”, author=“Mads”)
 
my_calculator = McStasScript(parameters=my_parameters,
inpath=“/path/to/input/data”, outpath=“/path/to/output/data”)
 
src = my_calculator.add_component(“source”, “source_simple”)
src.xwidth = 0.1
src.yheight = 0.1
src.E0 = 10
src.dE = 2
 
my_calculator.add_parameter(“theta”, value=10)
 
mono = my_calculator.add_component(“mono”, “Monochromator_flat”)
mono.xwidth = 0.03
mono.yheight = 0.05
mono.Q = 1.22
mono.set_AT([0, 0, 1], RELATIVE=“source”)
mono.set_ROTATED([0, “theta”, 0], RELATIVE=“source”)
 
my_calculator.add_declare_var(“two_theta”)
my_calculator.append_initialize(“two_theta = 2.0*theta;”)
 
beam_dir = my_calculator.add_component(“beam_dir”, “Arm”)
beam_dir.set_AT([0,0,0], RELATIVE=“mono”)
beam_dir.set_ROTATED([0,”two_theta”,0], RELATIVE=“source”)
 
my_calculator.run(input = {“theta”: 25))
 
data = my_calculator.data
```
