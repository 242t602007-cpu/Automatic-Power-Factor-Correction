# Automatic-Power-Factor-Correction
import math
import time

# Automatic Power Factor Correction

VOLTAGE = 230       # Volts
CURRENT = 10        # Amps
REAL_POWER = 1500   # Watts

# Available capacitor steps in kVAR
capacitors = [0.5, 1.0, 2.0, 3.0]

# Calculate apparent power
apparent_power = VOLTAGE * CURRENT

# Calculate initial power factor
power_factor = REAL_POWER / apparent_power

print("AUTOMATIC POWER FACTOR CORRECTION")
print("----------------------------------")
print("Voltage       :", VOLTAGE, "V")
print("Current       :", CURRENT, "A")
print("Real Power    :", REAL_POWER, "W")
print("Initial PF    :", round(power_factor, 3))

# Target power factor
target_pf = 0.95

if power_factor < target_pf:

    # Required reactive power
    phi1 = math.acos(power_factor)
    phi2 = math.acos(target_pf)

    required_kvar = (
        REAL_POWER * (math.tan(phi1) - math.tan(phi2))
    ) / 1000

    print("Required Capacitor:", round(required_kvar, 3), "kVAR")

    # Select capacitor
    selected = 0

    for capacitor in capacitors:
        if capacitor <= required_kvar:
            selected = capacitor

    print("Capacitor Connected:", selected, "kVAR")
    print("Power Factor Corrected")

else:
    print("Power factor is already good.")
    print("No capacitor required.")

print("----------------------------------")
