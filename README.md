# Instrument_Codes
This repository contains all the drivers and codes I contributed to writing.
# DynaCool_14T.py
The Dynacool document is mostly borrowed from Qcode repository. The issue for using the code from the repository is PPMS DynaCool has different returning structure for different model. This code is now compatible specifically with PPMS 14T system. 

ref. https://microsoft.github.io/Qcodes/drivers_api/QuantumDesign.html#qcodes.instrument_drivers.QuantumDesign.DynaCool
## Example Usage
from Drivers.DynaCool_14T import DynaCool
dynacool = DynaCool('dynacool', address="TCPIP0::10.155.94.51::5000::SOCKET")

def set_field(target, rate, method = 'non-blocking'):
    dynacool.field_target(target)
    dynacool.field_rate(rate)
    dynacool.ramp(method)
def set_temp(target,rate,method = 'fast settle'): 
    '''
    Target unit: K 
    rate unit: K/min
    method: 'fast settle', 'no overshoot'
    '''
    dynacool.temperature_rate(rate/60)
    dynacool.temperature_setpoint(target)
    dynacool.temperature_settling(method)

set_field(0.0,60/1e4)
set_temp(2,1)
