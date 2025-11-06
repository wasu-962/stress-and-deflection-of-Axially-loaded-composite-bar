# AXIALLY LOADED COMPOSITE BAR (STEEL + BRASS)
# ------------------------------------------------------------
# Given:
#   - Brass: outer diameter = 30 mm, inner diameter = 20 mm
#   - Steel: solid diameter = 12 mm
#   - E_steel = 210 GPa
#   - E_brass = 105 GPa
#
# Required:
#   (i)  Maximum normal stress in each material
#   (ii) Displacement of free end
#
# NOTE: Adjust 'L_steel', 'L_brass', and 'P' to match your problem.
# ============================================================

import math

# ----------------------------
# INPUT DATA
# ----------------------------
# Lengths of each segment (m)
L_steel = 0.4    # example: 400 mm → 0.4 m
L_brass = 0.6    # example: 600 mm → 0.6 m

# Applied axial load (N)
P = 40000        # example: 40 kN load in tension

# Material properties (Pa)
E_steel = 210e9   # 210 GPa
E_brass = 105e9   # 105 GPa

# Cross-sectional dimensions (mm)
d_steel = 12      # solid
D_brass_outer = 30
D_brass_inner = 20

# ----------------------------
# CALCULATIONS
# ----------------------------

# Convert diameters from mm → m
d_steel_m = d_steel / 1000
D_b_o_m = D_brass_outer / 1000
D_b_i_m = D_brass_inner / 1000

# Cross-sectional areas (m²)
A_steel = math.pi * (d_steel_m**2) / 4
A_brass = math.pi * (D_b_o_m**2 - D_b_i_m**2) / 4

# Stress in each segment (σ = P / A)
stress_steel = P / A_steel
stress_brass = P / A_brass

# Elongation (δ = PL / AE)
delta_steel = P * L_steel / (A_steel * E_steel)
delta_brass = P * L_brass / (A_brass * E_brass)

# Total elongation of bar
delta_total = delta_steel + delta_brass

# ----------------------------
# OUTPUT
# ----------------------------
print("===== RESULTS =====")
print(f"Steel area = {A_steel*1e6:.3f} mm²")
print(f"Brass area = {A_brass*1e6:.3f} mm²\n")

print(f"Stress in steel = {stress_steel/1e6:.2f} MPa")
print(f"Stress in brass = {stress_brass/1e6:.2f} MPa\n")

print(f"Elongation in steel = {delta_steel*1e3:.4f} mm")
print(f"Elongation in brass = {delta_brass*1e3:.4f} mm")
print(f"Total elongation (free-end displacement) = {delta_total*1e3:.4f} mm")
