# An example for a calculator
```py
# The `base_path` of a calculator is "./" by default. This attribute is introduced here for `instrument.set_base_path`
my_source.set_base_path('./')

# Set a Gaussian Source
# When the calculator is instantiated, the default parameters will also be set.
my_source = GaussWavefrontCaclulator('my_source')

# All the parameters can be viewed with this function, showing the limit, unit and value of each parameter:
my_source.list_parameters()
# The value of a certain parameter can be modified by:
my_source.parameters['photon_energy'].set_value(10)
my_source.parameters['photon_energy_relative_bandwidth'].set_value(1e-3)
my_source.parameters['number_of_transverse_grid_points'].set_value(400)

my_source.backengine()
my_source.saveH5('h5_data')
```

# An example for an instrument
```py
# Instantiate a instrument
my_instrument = Instrument('myInstrument')

# Add calculators
my_instrument.add_calculator(calculator1)
my_instrument.add_calculator(calculator2)
my_instrument.add_calculator(calculator3)

# List all the calculators
my_instrument.list_calculators()

# Remove a calculator
my_instrument.remove_calculator(calculator1.name)

# Dump the parameters into .json
my_instrument.parameters.to_json('instr_parameters.json')
```
