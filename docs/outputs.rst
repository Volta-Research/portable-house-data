Portable House Data Outputs
===========================

The portable house data output json structure is designed to contain the results of modelled energy performance. 
It is an optional add-on to the inputs section of the portable house data file.


Compatibility
*************

Document last updated for schema version *v1.0.2*


Outputs
-------

All outputs are reported on an annual basis unless otherwise noted.

  ==================================  ========  =======  ===========  ============================================================
  Variable Name                       Type      Units    Constraints  Notes
  ==================================  ========  =======  ===========  ============================================================
  ``totalEnergyConsumption``          double    GJ                    The total energy consumption calculated as the sum of the heating, cooling, ventilation, hot water, and base load energy consumption.                                    
  ``totalOperationalEmissions``       double    tCO2e                 Total annual operational emissions of the dwelling associated with the consumption of electricity, natural gas, propane, oil, and wood                                       
  ``designHeatLoss``                  double    kW                    The design heat loss of the building                                                 
  ``designHeatLossUnits``             string             kW, BTU/h    Units of reported design heat loss                                                             
  ``designHeatLossTemp``              double    ˚C                    Design temperature used to calculate design heat loss                                           
  ``designHeatGain``                  double    kW                    The design heat gain of the building                                                 
  ``designHeatGainUnits``             string             kW, BTU/h    Units of reported design heat gain                                                                  
  ``designHeatGainTemp``              double    ˚C                    Design temperature used to calculate design heat gain                                            
  ``heatLossWindows``                 double    GJ                    Gross heat loss through windows                                                    
  ``heatLossDoors``                   double    GJ                    Gross heat loss through doors                                                  
  ``heatLossAir``                     double    GJ                    Gross heat loss from air infiltration and mechanical ventilation                                                
  ``heatLossFloor``                   double    GJ                    Gross heat loss through exposed floors                                                   
  ``heatLossWalls``                   double    GJ                    Gross heat loss through above grade walls                                                  
  ``heatLossFoundationWalls``         double    GJ                    Gross heat loss through foundation walls                                                            
  ``heatLossFoundationSlab``          double    GJ                    Gross heat loss through foundation slabs                                                           
  ``heatLossCeiling``                 double    GJ                    Gross heat loss through ceilings                                                    
  ``heatLossFoundationTotal``         double    GJ                    Gross heat loss through the entire foundation                                                            
  ``totalCoolingEnergy``              double    GJ                    Annual cooling energy consumption                                                       
  ``totalHeatingEnergy``              double    GJ                    Annual heating energy consumption                                                       
  ``totalHotWaterEnergy``             double    GJ                    Annual hot water energy consumption                                                        
  ``totalBaseloadEnergy``             double    GJ                    Annual base load energy consumption                                                        
  ``totalVentilationEnergy``          double    GJ                    Annual ventilation energy consumption                                                           
  ``totalElectricalEnergy``           double    kWh                   Total annual electricity consumption                                                          
  ``totalNaturalGasEnergy``           double    m³                    Total annual natural gas consumption                                                           
  ``totalPropaneEnergy``              double    L                     Total annual propane consumption                                                       
  ``totalOilEnergy``                  double    L                     Total annual oil consumption                                                       
  ``totalWoodEnergy``                 double    kg                    Total annual wood consumption                                                     
  ``totalOnSiteGeneration``           double    kWh                   Total annual onsite electricity generation (from solar PV)                                                           
  ==================================  ========  =======  ===========  ============================================================
