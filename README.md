# Instrument_Codes

This repository contains Python instrument drivers and automation codes that I contributed to writing, specifically for Quantum Design's **PPMS DynaCool 14T** system.

---

## DynaCool_14T.py

This driver is adapted from the [Qcodes repository](https://microsoft.github.io/Qcodes/drivers_api/QuantumDesign.html#qcodes.instrument_drivers.QuantumDesign.DynaCool), with modifications to support the **PPMS DynaCool 14T** system.

**Note:** Different models of DynaCool systems return slightly different response formats. This code is tailored for **PPMS 14T** and may not work out-of-the-box with other models.

---

## Example Usage

```python
from Drivers.DynaCool_14T import DynaCool

# Initialize instrument
dynacool = DynaCool('dynacool', address="TCPIP0::10.155.94.51::5000::SOCKET")

# Set magnetic field
def set_field(target, rate, method='non-blocking'):
    dynacool.field_target(target)
    dynacool.field_rate(rate)
    dynacool.ramp(method)

# Set temperature
def set_temp(target, rate, method='fast settle'):
    """
    Set temperature on DynaCool.

    Parameters:
        target (float): Target temperature in Kelvin.
        rate (float): Temperature ramp rate in K/min.
        method (str): Settling method, e.g., 'fast settle' or 'no overshoot'.
    """
    dynacool.temperature_rate(rate / 60)  # Convert to K/s
    dynacool.temperature_setpoint(target)
    dynacool.temperature_settling(method)

# Example calls
set_field(0.0, 60 / 1e4)
set_temp(2, 1)
```

---

## 🔗 Reference

- [Qcodes DynaCool Driver Documentation](https://microsoft.github.io/Qcodes/drivers_api/QuantumDesign.html#qcodes.instrument_drivers.QuantumDesign.DynaCool)
