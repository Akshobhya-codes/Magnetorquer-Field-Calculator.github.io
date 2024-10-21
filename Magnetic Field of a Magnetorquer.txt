#Note: This is an IDLE Python File and should be opened through
#IDLE Python only otherwise it may fail to open/work efficiently

#Imports
import math  # Importing the math library for numerical operations

# Constants
I = 0.5  # Current in Amperes
ur = 800  # Relative permeability of the core material
u0 = (4 * math.pi) / (10**7)  # Permeability of free space (H/m)
r = 4.75 / 1000  # Convert radius from mm to meters

# Constant term for magnetic field calculation
numconst = (ur * u0 * I * r * r) / 2  # Pre-calculated constant

ltot = 103 / 1000  # Convert total length from mm to meters
initial_z = 3.5 / 1000 - ltot / 229  # Convert initial offset to meters
B_values = []  # List to store B values
z_values = []  # List to store corresponding z values

# Loop to calculate magnetic field for 12 specific z positions
for i in range(12):
    z = initial_z + (i * ltot / 11)  # Increment z position (11 to get 12 values)
    # Calculate magnetic field contribution from this z position
    B = (numconst) / math.pow((r * r + z * z), 1.5)
    B_values.append(B)  # Store the magnetic field value
    z_values.append(z * 1000)  # Store the z value in mm for display

# Output the results
for z, B in zip(z_values, B_values):
    print(f"For z value {round(z, 4)} mm, B is: {round(B * 1000, 6)} N/Amm")  # Convert B to N/Amm

# Final total B value across all z positions (optional)
total_B = sum(B_values)
print(f"\nFinal total B value: {round(total_B * 2000, 6)} T")  # Final magnetic field in Tesla
