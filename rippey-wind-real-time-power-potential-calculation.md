#################################################
Rippey Wind Real-Time Power Potential Calculation
#################################################

| Nick Moe
| Manager of SCADA Engineering
| Consulting Engineers Group

********
Overview
********

The SEL-3530 RTAC at Rippey contains code written by Nicholas Moe of CEG to calculate the real-time power potential. The code essentially implements a real-time lookup of potential power values from tables provided by Nordex.

The tables list values of power potential in kW for any given combination of wind speed in m/s and air density in kg/m³. The wind speeds covered by the tables range from 3 to 25 m/s, inclusive, in increments of 0.5 m/s. The air densities covered by the tables range from 1.000 to 1.300 kg/m³, inclusive, in increments of 0.025 kg/m³.

***********
Air Density
***********

The met tower data logger calculates air density, in kg/m³, using the following formula:

.. math::

   \rho = \frac{P}{R_\text{air}(T + 273.15)}

where :math:`\rho` is the air density in kg/m³, :math:`P` is atmospheric pressure in Pa, :math:`R_\text{air}` is the specific gas constant for dry air, 287.05 J⋅kg⁻¹⋅K⁻¹, and :math:`T` is the air temperature in °C.

The logger provides the RTAC with two air density values, notated A1 and B1. The logger calculates the A1 value with measurements from the A1 sensors, and calculates the B1 value with measurements from the B1 sensors. The A1 and B1 notations refer to groups of sensors on the met tower. It is unknown to me what heights they are at or on what side of the met tower they are.

The RTAC uses the average of the two air density values as an input to the real-time power potential determination.

**********
Wind Speed
**********

The RTAC gathers wind speeds from each turbine in m/s. It uses that wind speed in the real-time power potential lookup.

If that wind speed value is not available because the comms with that turbine are offline or data is not available for some reason, the RTAC substitutes an average wind speed from all turbines that are reporting wind speed with good quality.

**********************
Power Potential Lookup
**********************

The RTAC performs a lookup of power potential for each turbine with the wind speed and air density values described above.

Each turbine is assigned a boolean that lets the RTAC know if the turbines is to be considered available or not. At Rippey, all turbines are currently assumed to be available. If a turbine is marked as not available, the power potential for that turbine is assumed to be zero.

If the turbine is available, the RTAC performs the lookup as follows:

1. Round the wind speed down to the nearest 0.5 m/s.
#. Round the air density to the nearest 0.025 kg/m³.
#. Filter out conditions not covered by the tables:

   a. If the wind speed is below 3 m/s or above 25 m/s, the assume the power potential to be zero and perform no further lookups. Anything below 3 m/s is assumed to be not enough for meaningful production, and it is assumed that the turbines cut out above 25 m/s.
   #. If the air density is below 1.000 kg/m³, assume the air density to be 1.000 kg/m³ for the purposes of the lookup.
   #. If the air density is above 1.300 kg/m³, assume the air density to be 1.300 kg/m³ for the purposes of the lookup.

#. Find the column in the table corresponding to the rounded air density.
#. In that column, find the power potential corresponding to the rounded wind speed.

***************
Final Summation
***************

After finding the power potential for the turbine, the RTAC sums the power potentials by feeder:
   
   :Feeder 1: Turbines 4, 5, 6, 7, 8, 9, 10, 11, 12, 13
   :Feeder 2: Turbines 1, 2, 3, 14, 15, 16, 17, 18, 19, 20

The RTAC then sends these sums to the SEL-3354 running Subnet, which then passes the data on to CES.
