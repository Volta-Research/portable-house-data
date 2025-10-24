Portable House Data Inputs
==========================

The portable house data input file (json format) is designed to be flexible, allowing buildings to be defined at a variety of levels of detail. 
Where parameters are not required, recommended defaults are provided. 
However, it falls on the individual software provider or data interpreter to handle defaults within their own systems appropriately.

The file format contains two levels of nesting: *Category* and *Object Class*. *Categories* include: Building Information, Building Site, Enclosure, Systems, and Occupant Characteristics.

The **Required** field in the table below indicates whether a parameter is required in the context of that object class, but not all Object Classes are required. 
For example, if the ``foundation`` object class is included, the ``foundationType`` variable is also required. 
Object classes that are required indicate so in their section headers below.


Data Provenance
***************

Throughout the Portable House Data standard, data provenance can be tracked through the inclusion of an optional "_src" tag appended to the end of a field key. 
This tag can be used be service providers to provide additional context as to the source of data, and can assist in tracking changes to the data over its lifetime. 
An example of how data provenance may be included is shown below::

    {
        ...
        "foundation": {
            "foundationType": "basement",
            "foundationFloorArea": 60,
            "foundationFloorArea_src": "Measured-HOT2000"
        }
    }

Content of `_src` fields must be in string format, but the content itself is not prescribed.

Building Information
--------------------

The object key for this section is ``buildingInfo``.

Building Specifications (REQUIRED)
**********************************

The object key for this section is ``specifications``.

The Building Specifications section is always required, meaning that the ``yearBuilt`` and ``totalConditionedFloorArea`` of the home are always required parameters

  ==================================  ========  =======  ===========  ========  ===========  ============================================================
  Variable Name                       Type      Units    Constraints  Required  Default      Notes
  ==================================  ========  =======  ===========  ========  ===========  ============================================================
  ``yearBuilt``                       integer                         Yes                    Year built of dwelling unit
  ``planShape``                       string             See [#]_     No        rectangular  Shape of home. Includes number of corners, aligned with ERS
  ``buildingType``                    string             See [#]_     No        detached     Type of dwelling
  ``facingDirection``                 string             See [#]_     No        S            Front-facing direction of building
  ``numConditionedFloors``            integer            > 0, <=4     No        1            Total number of storeys, including basement if applicable
  ``numConditionedFloorsAboveGrade``  integer            >= 0, <=3    No        1            Total number of above grade storeys
  ``layoutType``                      string             See [#]_     No        standard     Layout of storeys, used to indicate presence of split levels
  ``totalConditionedFloorArea``       double    m²       >0, <=600    Yes                    Total conditioned floor area of the building
  ==================================  ========  =======  ===========  ========  ===========  ============================================================

  .. [#] ``layoutType`` choices are "standard" and "split".
  .. [#] ``planShape`` choices are "rectangular", "t-shape", "l-shape", "5-6 corners", "7-8 corners", "9-10 corners", and "11 or more corners"
  .. [#] ``buildingType`` choices are "detached", "attached", "row-middle", "row-end", "murb unit", and "murb building"
  .. [#] ``facingDirection`` choices are "N", "NE", "E", "SE", "S", "SW", "W", and "NW"



Building Site
-------------

The object key for this section is ``buildingSite``.

Location (REQUIRED)
***********************

The object key for this section is ``location``.

Location information can be entered in four different ways depending on the level of detail provided.
These sections can be used in combination with eachother, but at least one of the following sets of data is required.

Address
~~~~~~~
  
  ==================================  ========  =======  ===========  ========  ===========  =============================================================
  Variable Name                       Type      Units    Constraints  Required  Default      Notes
  ==================================  ========  =======  ===========  ========  ===========  =============================================================
  ``address``                         string                          No                     Combination of the below three options (e.g. 123 Fake Street)
  ``addressCivicNumber``              string                          No                     Address number (e.g. 123, 2A)
  ``addressStreetName``               string                          No                     Address street name (e.g. Fake Street)
  ``addressUnitNumber``               string                          No                     Unit number, if applicable
  ==================================  ========  =======  ===========  ========  ===========  =============================================================

Postal Code
~~~~~~~~~~~
The postal code input allows either a full postal code (6 characters or 7 with a space), or the forward sortation area (FSA, first three digits of the postal code). 
  
  ==================================  ========  =======  =============  ========  ===========  ============================================================
  Variable Name                       Type      Units    Constraints    Required  Default      Notes
  ==================================  ========  =======  =============  ========  ===========  ============================================================
  ``postalCode``                      string             >=3, <7 char.  No                     Building's postal code or FSA
  ==================================  ========  =======  =============  ========  ===========  ============================================================

Region
~~~~~~~~~~~
  
  ==================================  ========  =======  =============  ========  ===========  ============================================================
  Variable Name                       Type      Units    Constraints    Required  Default      Notes
  ==================================  ========  =======  =============  ========  ===========  ============================================================
  ``city``                            string                            No                     City, town, or village name
  ``region``                          string             See [#]_       No                     Province, Territory, or State
  ``country``                         string                            No        CANADA       Country
  ==================================  ========  =======  =============  ========  ===========  ============================================================

  .. [#] ``region`` should use two-letter province/territory/state abbreviation ("ON", "QC", "YT", etc.)

Latitude & Longitude
~~~~~~~~~~~~~~~~~~~~
  
  ==================================  ========  =======  =============  ========  ===========  ============================================================
  Variable Name                       Type      Units    Constraints    Required  Default      Notes
  ==================================  ========  =======  =============  ========  ===========  ============================================================
  ``latitude``                        double    WGS84                   No                     Latitude of building
  ``longitude``                       double    WGS84                   No                     Longitude of building
  ==================================  ========  =======  =============  ========  ===========  ============================================================


Enclosure
---------

The object key for this section is ``enclosure``.


Air Infiltration
***********************

The object key for this section is ``airInfiltration``.

  ==================================  ========  =======  =============  ========  ===========  =================================================================
  Variable Name                       Type      Units    Constraints    Required  Default      Notes
  ==================================  ========  =======  =============  ========  ===========  =================================================================
  ``airLeakageRate``                  double    ACH50    >0             No        See [#]_     Air leakage of dwelling
  ``airLeakageRateAssumed``           boolean                           No        true         Whether the provided value is assumed (true) or measured (false)
  ==================================  ========  =======  =============  ========  ===========  =================================================================

  .. [#] ``airLeakageRate`` defaults are not provided, assuming interpreters have a means of assuming defaults where measured values are not provided (e.g. ERS Technical Procedures Appendix D).



Foundation
***********************

The object key for this section is ``foundation``.

  ==================================  ========  =======  =============  ========  ===========  ============================================================
  Variable Name                       Type      Units    Constraints    Required  Default      Notes
  ==================================  ========  =======  =============  ========  ===========  ============================================================
  ``foundationType``                  string             See [#]_       Yes                    Type of foundation [#]_
  ``foundationPerimeter``             double    m        >0             No                     Foundation exposed perimeter
  ``foundationFloorArea``             double    m²       >0             No                     Foundation floor area                     
  ``foundationWallHeight``            double    m        >0             No                     Foundation total wall height (slab to ceiling)     
  ``foundationWallDepth``             double    m        >0             No                     Foundation wall depth (slab to grade)    
  ``foundationWallInsulation``        double    RSI      >0             No                     Foundation wall effective insulation value 
  ``foundationSlabInsulation``        double    RSI      >0             No                     Foundation slab effective insulation value
  ==================================  ========  =======  =============  ========  ===========  ============================================================

  .. [#] ``foundationType`` choices are "basement", "crawlspace", "slab-on-grade", "walkout", and "piers". The "crawlspace" foundation type represents enclosed crawlspaces, while the "piers" foundation type includes vented crawlspaces.
  .. [#] For dwellings with complex foundations made up of multiple types, the dominant foundation (based on floor area) should be indicated. 

Walls
***********************

The object key for this section is ``walls``.

  ==================================  ========  =======  =============  ========  ===========  ============================================================
  Variable Name                       Type      Units    Constraints    Required  Default      Notes
  ==================================  ========  =======  =============  ========  ===========  ============================================================
  ``wallTotalArea``                   double    m²       >0             No                     Total surface area of above grade walls
  ``wallInsulation``                  double    RSI      >0             No                     Effective insulation value within above grade walls
  ==================================  ========  =======  =============  ========  ===========  ============================================================


Attic Ceilings
***********************

The object key for this section is ``atticCeilings``.

When no information on ceilings is provided, a ceiling with an attic is recommended to be assumed.

  ==================================  ========  =======  =============  ========  ===========  ============================================================
  Variable Name                       Type      Units    Constraints    Required  Default      Notes
  ==================================  ========  =======  =============  ========  ===========  ============================================================
  ``ceilingArea``                     double    m²       >0             No                     Surface area of ceiling 
  ``ceilingInsulation``               double    RSI      >0             No                     Effective insulation value within attic
  ==================================  ========  =======  =============  ========  ===========  ============================================================

Flat Ceilings
***********************

The object key for this section is ``flatCeilings``.

  ==================================  ========  =======  =============  ========  ===========  ============================================================
  Variable Name                       Type      Units    Constraints    Required  Default      Notes
  ==================================  ========  =======  =============  ========  ===========  ============================================================
  ``ceilingArea``                     double    m²       >0             No                     Surface area of ceiling 
  ``ceilingInsulation``               double    RSI      >0             No                     Effective insulation value within flat ceilings
  ==================================  ========  =======  =============  ========  ===========  ============================================================

Cathedral Ceilings
***********************

The object key for this section is ``cathedralCeilings``.

  ==================================  ========  =======  =============  ========  ===========  ============================================================
  Variable Name                       Type      Units    Constraints    Required  Default      Notes
  ==================================  ========  =======  =============  ========  ===========  ============================================================
  ``ceilingArea``                     double    m²       >0             No                     Surface area of ceiling 
  ``ceilingInsulation``               double    RSI      >0             No                     Effective insulation value within cathedral ceilings
  ==================================  ========  =======  =============  ========  ===========  ============================================================

Exposed Floor
***********************

The object key for this section is ``exposedFloors``.

  ========================================  ========  =======  =============  ========  ===========  ==================================================================================================
  Variable Name                             Type      Units    Constraints    Required  Default      Notes
  ========================================  ========  =======  =============  ========  ===========  ==================================================================================================
  ``exposedFloorAdjacentConditionedSpace``  boolean                           No        false        Indicates if the underside of the exposed floor is above a space such as an enclosed garage.
  ``exposedFloorArea``                      double    RSI      >=0            No                     Horizontal surface area of exposed floor
  ``exposedFloorInsulation``                double    RSI      >=0            No                     Effective insulation value of exposed floor
  ========================================  ========  =======  =============  ========  ===========  ==================================================================================================

Windows
***********************

The object key for this section is ``windows``.

  ==================================  ========  ========  =============  ========  ===========  ===========================================================================================================================
  Variable Name                       Type      Units     Constraints    Required  Default      Notes
  ==================================  ========  ========  =============  ========  ===========  ===========================================================================================================================
  ``numWindows``                      integer   count     >0             No                     Total window count
  ``windowArea.total``                double    m²        >0             No                     Total window area for the entire building
  ``windowArea.south``                double    m²        >0             No                     Total window area on the south face of the building
  ``windowArea.southeast``            double    m²        >0             No                     Total window area on the southeast face of the building
  ``windowArea.east``                 double    m²        >0             No                     Total window area on the east face of the building
  ``windowArea.northeast``            double    m²        >0             No                     Total window area on the northeast face of the building
  ``windowArea.north``                double    m²        >0             No                     Total window area on the north face of the building
  ``windowArea.northwest``            double    m²        >0             No                     Total window area on the northwest face of the building
  ``windowArea.west``                 double    m²        >0             No                     Total window area on the west face of the building
  ``windowArea.southwest``            double    m²        >0             No                     Total window area on the southwest face of the building
  ``glassLayerType``                                      See [#]_       No                     Description of the glass layers of the window
  ``frameType``                                           See [#]_       No                     
  ``coatingType``                                         See [#]_       No                     
  ``fillGasType``                                         See [#]_       No                     Type of gas inside double/triple-pane windows. Ignored for single-pane.
  ``overallUValue``                   double    W/(m²K)                  No                     Full-assembly U-factor of the window
  ``shgc``                            double    fraction                 No                     Full-assembly solar heat gain coefficient of the window
  ``fractionOperable``                double    fraction  >=0, <=1       No        0            Area fraction of windows that are operable. Calculated as the total operable window area divided by the total window area
  ==================================  ========  ========  =============  ========  ===========  ===========================================================================================================================
  
  .. [#] ``glassLayerType`` choices are "single-pane", "double-pane", "triple-pane", or "glass block".
  .. [#] ``frameType`` choices are "aluminum", "fiberglass", "metal", "vinyl", or "wood".
  .. [#] ``coatingType`` choices are "clear", "low-e", "low-e, high-solar-gain", "low-e, low-solar-gain", "tinted", "tinted/reflective", or "reflective"
  .. [#] ``fillGasType`` choices are "air", "argon", "krypton", "other".

It is recommended that either a description of the window is provided using the fields: ``glassLayerType``, ``frameType``, ``coatingType``, and ``fillGasType``, or the windows are described using ``overallUValue`` and ``shgc``

Doors
***********************

The object key for this section is ``doors``.

  ==================================  ========  ========  =============  ========  ===========  ========================
  Variable Name                       Type      Units     Constraints    Required  Default      Notes
  ==================================  ========  ========  =============  ========  ===========  ========================
  ``numDoors``                        integer   count     >0             No                     Total door count
  ``numPatioDoors``                   integer   count     >=0            No                     Total patio door count
  ``doorUValue``                      double    W/(m²K)   >0             No                     
  ``patioDoorUValue``                 double    W/(m²K)   >0             No                     
  ==================================  ========  ========  =============  ========  ===========  ========================



Systems
-------

The object key for this section is ``systems``

Primary Heating
***********************

The object key for this section is ``primaryHeating``.

When the primary heating system of a house is a heat pump, this section should be used to describe the heat pump's back-up or auxiliary heating system.

  ==================================  ========  ========  =============  ========  ===========  ================================================
  Variable Name                       Type      Units     Constraints    Required  Default      Notes
  ==================================  ========  ========  =============  ========  ===========  ================================================
  ``equipmentType``                                       See [#]_       Yes                                                             
  ``equipmentSubType``                                    See [#]_       No                                      
  ``fuelType``                                            See [#]_       Yes                                                             
  ``efficiency``                      double    %                        No                                                                
  ``capacity``                                                           No        kW           When units aren't provided, assumed to be kW                                              
  ``capacityUnits``                                       kW, BTU/h      No                                                                      
  ``manufacturerName``                string                             No                                                                  
  ``modelNumber``                     string                             No                                                                    
  ``ageOfEquipment``                  integer   years                    No                                                                                                                             
  ``ducted``                          boolean                            No                                                               
  ==================================  ========  ========  =============  ========  ===========  ================================================

  .. [#] ``equipmentType`` choices are "furnace", "boiler", "electric resistance", "wood stove", "fireplace", and "combination boiler".
  .. [#] ``equipmentSubType`` choices are "condensing", "non-condensing", "storage tank", and "tankless". The field may also be left empty if none apply.
  .. [#] ``fuelType`` choices are "electricity", "natural gas", "propane", "oil", "wood", "wood pellets".

The following table outlines permissible combinations of ``equipmentType``, ``equipmentSubType``, and ``fuelType`` options

  =========================== ======================================== =================
  ``type``                    ``equipmentSubType``                     ``fuelType``
  =========================== ======================================== =================
  furnace                     condensing, non-condensing               "electricity", "natural gas", "propane", "oil", "wood", "wood pellets"
  boiler                      condensing, non-condensing               "electricity", "natural gas", "propane", "oil", "wood", "wood pellets"
  electric resistance         None (field ignored)                     "electricity"
  wood stove                  None (field ignored)                     "wood", "wood pellets"
  fireplace                   None (field ignored)                     "wood", "wood pellets"
  combination boiler          storage tank, tankless                   "natural gas", "propane", "oil"
  =========================== ======================================== =================


Secondary Heating
***********************

The object key for this section is ``secondaryHeating``.

This section should only be used if information about the primary heating system is provided. It should not be used to model an auxiliary or backup system for a heat pump.

  ==================================  ========  ========  =============  ========  ===========  ================================================
  Variable Name                       Type      Units     Constraints    Required  Default      Notes
  ==================================  ========  ========  =============  ========  ===========  ================================================
  ``equipmentType``                                       See [#]_       Yes                                                             
  ``equipmentSubType``                                    See [#]_       No                                      
  ``fuelType``                                            See [#]_       Yes                                                             
  ``efficiency``                      double    %                        No                                                                
  ``capacity``                                                           See [#]_  kW           When units aren't provided, assumed to be kW                                              
  ``capacityUnits``                                       kW, BTU/h      No                                                                      
  ``manufacturerName``                string                             No                                                                  
  ``modelNumber``                     string                             No                                                                    
  ``ageOfEquipment``                  integer   years                    No                                                                                                                             
  ``ducted``                          boolean                            No                                                               
  ``heatedFloorArea``                 double    m²        >0             See [#]_
  ==================================  ========  ========  =============  ========  ===========  ================================================

  .. [#] ``equipmentType`` choices are "furnace", "boiler", "electric resistance", "wood stove", "fireplace", and "combination boiler".
  .. [#] ``equipmentSubType`` choices are "condensing", "non-condensing", "storage tank", and "tankless". The field may also be left empty if none apply.
  .. [#] ``fuelType`` choices are "electricity", "natural gas", "propane", "oil", "wood", "wood pellets".
  .. [#] .. [#] Either ``capacity`` or ``heatedFloorArea`` should be provided for a secondary heating system.


Permanent Cooling
***********************

The object key for this section is ``permanentCooling``.

  ==================================  ========  ========  ===============  ==============  ===========  ================================================
  Variable Name                       Type      Units     Constraints      Required        Default      Notes
  ==================================  ========  ========  ===============  ==============  ===========  ================================================
  ``equipmentType``                   string              See [#]_         No              central      The type of permanent cooling system                                
  ``efficiency``                      double    SEER                       No                           The efficiency of the cooling system, assumed to be in SEER when no units are provided                                     
  ``efficiencyUnits``                 string              COP,SEER,SEER2   No              SEER         Units of the provided cooling efficiency                                        
  ``capacity``                        double    kW                                                      The capacity of the cooling system, assumed to be in kW when no units are provided                                         
  ``capacityUnits``                   string              kW, BTU/h        No              kW           Units of the provided cooling capacity                                             
  ``manufacturerName``                string                               No                           Manufacturer/brand name of the cooling system                                       
  ``modelNumber``                     string                               No                           Model name/number of the cooling system                                         
  ``ageOfEquipment``                  integer   years     >=0              No                           Age of the cooling system                                               
  ``cooledFloorArea``                 double    m²        >0               No                           The amount of floor area served by the cooling system. Should only be used if the cooling system does not service the entire dwelling.
  ``installed``                       boolean                              Yes (See [#]_)  false        A true/false indicator that can be used to indicate the presence of a permanent cooling system without any other parameters.
  ==================================  ========  ========  ===============  ==============  ===========  ================================================

  .. [#] ``equipmentType`` choices are "central", and "mini-split"
  .. [#] ``installed`` should be set to true if the presence of a cooling system is indicated without any other parameters, but is otherwise not required.


Temporary Cooling
***********************

The object key for this section is ``temporaryCooling``.

  ==================================  ========  ========  ===============  ==============  ===========  ================================================
  Variable Name                       Type      Units     Constraints      Required        Default      Notes
  ==================================  ========  ========  ===============  ==============  ===========  ================================================
  ``equipmentType``                   string              See [#]_         No              central      The type of temporary cooling system                                
  ``efficiency``                      double    SEER                       No                           The efficiency of the cooling system, assumed to be in SEER when no units are provided                                     
  ``efficiencyUnits``                 string              COP,SEER,SEER2   No              SEER         Units of the provided cooling efficiency                                        
  ``capacity``                        double    kW                                                      The capacity of the cooling system, assumed to be in kW when no units are provided                                         
  ``capacityUnits``                   string              kW, BTU/h        No              kW           Units of the provided cooling capacity                                             
  ``manufacturerName``                string                               No                           Manufacturer/brand name of the cooling system                                       
  ``modelNumber``                     string                               No                           Model name/number of the cooling system                                         
  ``ageOfEquipment``                  integer   years     >=0              No                           Age of the cooling system                                               
  ``cooledFloorArea``                 double    m²        >0               No                           The amount of floor area served by the cooling system. Should only be used if the cooling system does not service the entire dwelling.
  ``installed``                       boolean                              No (See [#]_)   false        A true/false indicator that can be used to indicate the presence of a permanent cooling system without any other parameters.
  ==================================  ========  ========  ===============  ==============  ===========  ================================================

  .. [#] ``equipmentType`` choices are "window", and "floor"
  .. [#] ``installed`` should be set to true if the presence of a cooling system is indicated without any other parameters, but is otherwise not required.

Heat Pump
***********************

The object key for this section is ``heatPump``.

  ====================================  ========  ========  ==============   ========  ===========  ==========================================================
  Variable Name                         Type      Units     Constraints      Required  Default      Notes
  ====================================  ========  ========  ==============   ========  ===========  ==========================================================
  ``type``                              string              See [#]_         Yes                    The type of heat pump based on its heat source/sink
  ``distributionType``                  string              See [#]_         No                     The type of distribution system used by the heat pump                          
  ``numberOfHeads``                     int       count                      No                     The number of indoor heads for mini-split and multi-split heat pumps              
  ``fuelType``                          string              See [#]_         No        electricity  The fuel source for the heat pump. Note that natural gas is highly unlikely to be supported by simulation engines unless otherwise noted.                            
  ``ratedHeatingEfficiency``            double    COP       >0               No                     Rated heating efficiency, typically at 8.33˚C/47˚F                                             
  ``ratedHeatingEfficiencyUnits``       string              COP,HSPF,HSPF2   No                     Units for heating efficiency provided                    
  ``ratedHeatingCapacity``              double    kW        >0               No                     Rated heating capacity, typically at 8.333˚C/47˚F                           
  ``ratedHeatingCapacityUnits``         string              kW, BTU/hr       No                     Units for the heating capacity provided         
  ``ratedHeatingTemp``                  double    ˚C        >-50             No        8.333˚C      Temperature point for the rated heating capacity and efficiency       
  ``coldClimateHeatingEfficiency``      double    COP       >0               No                     Cold climate heating efficiency, typically at -15˚C/5˚F                       
  ``coldClimateHeatingCapacity``        double    kW        >0               No                     Cold climate heating capacity, typically at -15˚C/5˚F                     
  ``coldClimateHeatingCapacityUnits``   string              kW, BTU/hr       No                     Units for the cold climate heating capacity provided                            
  ``coldClimateRatingTemp``             double    ˚C        >-50             No        -15˚C        Temperature point for the cold climate heating capacity and efficiency                    
  ``usedForCooling``                    boolean                              No        true         Whether or not the heat pump is used for cooling in addition to heating                                    
  ``ratedCoolingEfficiency``            double    COP       >0               No                     Rated cooling efficiency, typically at 35˚C/95˚F                                
  ``ratedCoolingEfficiencyUnits``       double    COP       COP,SEER,SEER2   No                     Units for the cooling efficiency provided                                   
  ``ratedCoolingCapacity``              double    kW        >0               No                     Rated cooling capacity, typically at 35˚C/95˚F                                         
  ``ratedCoolingCapacityUnits``         string              kW, BTU/hr       No                     Units for the cooling capacity provided                                                            
  ``ratedCoolingTemp``                  double    ˚C        >15              No        35˚C         Temperature rating point for the provided cooling capacity and efficiency                                               
  ``switchoverTemperature``             double    ˚C        >-50             No                     Switchover temperature in heating mode, below which the primary heating system is configured to run                                                  
  ``manufacturerName``                  string                               No                     Manufacturer name of the heat pump                                    
  ``modelNameNumber``                   string                               No                     Model name or number of the heat pump                                                                
  ``ageOfEquipment``                    integer   years     >=0, <100        No                     Age of the heat pump                                                                                                                         
  ====================================  ========  ========  ==============   ========  ===========  ==========================================================

  .. [#] ``type`` choices are "air-to-air", "air-to-water", "ground-to-air", and "water-to-air"
  .. [#] ``equipmentSubType`` choices are "central", "mini-split", and "multi-split"
  .. [#] ``fuelType`` choices are "electricity", and "natural gas"


Primary Domestic Hot Water (DHW)
********************************

The object key for this section is ``primaryHotWater``.

  ==================================  ========  ========  =============  ========  ===========  ==========================================================
  Variable Name                       Type      Units     Constraints    Required  Default      Notes
  ==================================  ========  ========  =============  ========  ===========  ==========================================================
  ``tankType``                        string              See [#]_       No                     The tank type of the DHW system                                                                  
  ``equipmentSubType``                string              See [#]_       No                     Whether the DHW system is condensing or not                                                                                 
  ``fuelType``                        string              See [#]_       Yes                    The fuel source for the DHW system                                                                       
  ``efficiency``                      double    EF        >0             No                     The efficiency of the DHW system                                                                      
  ``tankCapacity``                    double    L         >=0            No                     The tank capacity (size) of the DHW system                                                                        
  ``manufacturerName``                string                             No                     Manufacturer name of the DHW system                                                                  
  ``modelNumber``                     string                             No                     Model name or number of the DHW system                                                                    
  ``ageOfEquipment``                  integer             >=0, <100      No                     Age of the DHW system                                                                        
  ``tankSetpoint``                    double    ˚C        >20            No        55           The hot water setpoint for the system                                                                     
  ``fractionOfTank``                  double    frac      >=0, <=1       No                     The fraction of the tank or hot water load served by this DHW system (for use when multiple systems are present)                                                                                
  ==================================  ========  ========  =============  ========  ===========  ==========================================================

  .. [#] ``tankType`` choices are "storage tank", "tankless", "heat pump", and "combination boiler"
  .. [#] ``equipmentSubType`` choices are "condensing", "non-condensing"
  .. [#] ``fuelType`` choices are "electricity", "natural gas", "propane", "oil", "wood", "wood pellets", and "solar"

The following table outlines permissible combinations of ``tankType``, ``equipmentSubType``, and ``fuelType`` options. These constraints also apply to secondary DHW systems.

  =========================== ======================================== =================
  ``tankType``                ``equipmentSubType``                     ``fuelType``
  =========================== ======================================== =================
  storage tank                "condensing", "non-condensing"           "electricity", "natural gas", "propane", "oil", "wood", "wood pellets", "solar"                                    
  tankless                    "condensing", "non-condensing"           "electricity", "natural gas", "propane", "oil"                               
  heat pump                   None (field ignored)                     "electricity"
  combination boiler          None (field ignored)                     "natural gas", "propane", "oil"
  =========================== ======================================== =================



Secondary Domestic Hot Water (DHW)
**********************************

The object key for this section is ``secondaryHotWater``.

  ==================================  ========  ========  =============  ========  ===========  ==========================================================
  Variable Name                       Type      Units     Constraints    Required  Default      Notes
  ==================================  ========  ========  =============  ========  ===========  ==========================================================
  ``tankType``                        string              See [#]_       No                     The tank type of the DHW system                                                                  
  ``equipmentSubType``                string              See [#]_       No                     Whether the DHW system is condensing or not                                                                                 
  ``fuelType``                        string              See [#]_       Yes                    The fuel source for the DHW system                                                                       
  ``efficiency``                      double    EF        >0             No                     The efficiency of the DHW system                                                                      
  ``tankCapacity``                    double    L         >=0            No                     The tank capacity (size) of the DHW system                                                                        
  ``manufacturerName``                string                             No                     Manufacturer name of the DHW system                                                                  
  ``modelNumber``                     string                             No                     Model name or number of the DHW system                                                                    
  ``ageOfEquipment``                  integer             >=0, <100      No                     Age of the DHW system                                                                        
  ``tankSetpoint``                    double    ˚C        >20            No        55           The hot water setpoint for the system                                                                     
  ``fractionOfTank``                  double    frac      >=0, <=1       See [#]_               The fraction of the tank or hot water load served by this DHW system (for use when multiple systems are present)                                                                                
  ==================================  ========  ========  =============  ========  ===========  ==========================================================

  .. [#] ``tankType`` choices are "storage tank", "tankless", "heat pump", and "combination boiler"
  .. [#] ``equipmentSubType`` choices are "condensing", "non-condensing"
  .. [#] ``fuelType`` choices are "electricity", "natural gas", "propane", "oil", "wood", "wood pellets", and "solar"
  .. [#] When a secondary system is present it is highly recommended that its contribution to the hot water load is indicated.


Ventilation
************

The object key for this section is ``ventilation``.

  =======================================  ========  ========  =============  ========  ===========  ==========================================================
  Variable Name                            Type      Units     Constraints    Required  Default      Notes
  =======================================  ========  ========  =============  ========  ===========  ==========================================================
  ``bathroomFanCount``                     integer             >=0            No                     The number of bathroom fans in the dwelling                              
  ``rangeHoodFanCount``                    integer             >=0            No                     The number of range hood fans in the dwelling                               
  ``otherFanCount``                        integer             >=0            No                     The number of other ventilation fans in the dwelling                           
  ``recoveryVentilatorType``               string              See [#]_       No                     The type of recovery ventilator (heat or energy)                                
  ``recoveryVentilatorEfficiency``         double    %         >0, <100       No                     The heating efficiency (SRE) of the HRV/ERV
  ``recoveryVentilatorManufacturerName``   string                             No                     Manufacturer name of the HRV/ERV                             
  ``recoveryVentilatorModelNumber``        string                             No                     Model name/number of the HRV/ERV                               
  ``ageOfRecoveryVentilator``              integer   years     >0             No                     Age of the HRV/ERV                           
  =======================================  ========  ========  =============  ========  ===========  ==========================================================

  .. [#] ``recoveryVentilatorType`` choices are "none", "hrv", and "erv"



Solar Photovoltaics (PV)
*************************

The object key for this section is ``solarPv``.

  ==================================  ========  ========  =============  ========  ===========  ==========================================================
  Variable Name                       Type      Units     Constraints    Required  Default      Notes
  ==================================  ========  ========  =============  ========  ===========  ==========================================================
  ``mountingLocation``                string              See [#]_       No        roof         Location of the PV system                                                  
  ``systemOrientation``               double    degree                   No                     Orientation of the PV system, measured in degrees from North clockwise (northeast = 45˚)                                             
  ``systemTiltAngle``                 double    degree                   No                     Tilt angle of the PV system, measured in degrees from horizontal                                           
  ``systemCapacity``                  double    kW                       Yes                    Capacity (max power output) of the PV system                                      
  ``systemEfficiency``                double    %                        No                     Nominal efficiency of the PV system                                       
  ``ageOfEquipment``                  integer   years                    No                     Age of the PV system                                          
  ``numberOfPanels``                  integer   count                    No                     Number of individual panels                                          
  ``manufacturerName``                string                             No                     Manufacturer name of the PV system                               
  ``modelNumber``                     string                             No                     Model name/number of the PV system                                 
  ==================================  ========  ========  =============  ========  ===========  ==========================================================

  .. [#] ``mountingLocation`` choices are "roof", "ground", and "garage"


Energy Storage
*************************

The object key for this section is ``energyStorage``. 

This section is used to indicate the presence of a battery energy storage system.

  ==================================  ========  ========  =============  ========  ===========  ==========================================================
  Variable Name                       Type      Units     Constraints    Required  Default      Notes
  ==================================  ========  ========  =============  ========  ===========  ==========================================================
  ``batteryEnergyCapacity``           double    kWh       >0             Yes                    The amount of energy that can be stored in the battery bank                                                                  
  ``inverterCapacity``                double    kW        >0             Yes                    The nominal charge/discharge rate of the inverter                                                                 
  ``manufacturerName``                string                             No                     Manufacturer name of the battery energy storage system
  ``modelNumber``                     string                             No                     Model name/number of the battery energy storage system       
  ==================================  ========  ========  =============  ========  ===========  ==========================================================


Transportation
*************************

The object key for this section is ``transportation``. 

This section is used to indicate the presence of any electric vehicles.

  ==================================  ========  ========  =============  ========  ===========  ==========================================================
  Variable Name                       Type      Units     Constraints    Required  Default      Notes
  ==================================  ========  ========  =============  ========  ===========  ==========================================================
  ``electricVehicleCount``            integer   count     >0             Yes                    The number of electric vehicles charged at the dwelling                                                                 
  ``ageOfVehicle``                    integer   year      >0             No                     Age of vehicle                                                                  
  ``chargerCapacity``                 double    kW        >0             No                     Maximum rate of charge for the electric vehicle
  ``isBidirectional``                 boolean                            No        false        Whether the charger can draw power from the vehicle as a back-up source for the dwelling                        
  ``manufacturerName``                string                             No                     Manufacturer name of the primary electric vehicle
  ``modelNumber``                     string                             No                     Model name/number of the primary electric vehicle       
  ==================================  ========  ========  =============  ========  ===========  ==========================================================



Occupant Characteristics
------------------------

The object key for this section is ``occupancy``. 

  ===================================  ========  ========  =============  ========  ===========  ==========================================================
  Variable Name                        Type      Units     Constraints    Required  Default      Notes
  ===================================  ========  ========  =============  ========  ===========  ==========================================================
  ``totalOccupantCount``               integer   count     >0             Yes       See [#]_     The total number of occupants in the dwelling                                                                 
  ``occupantCountHomeDuringWeekdays``  integer   count     >=0            No        false        The total number of occupants in the dwelling expected to be home on weekdays (i.e. work-from-home occupants)                        
  ===================================  ========  ========  =============  ========  ===========  ==========================================================

  .. [#] It is recommended that 3 occupants are assumed for single family dwellings and 2 occupants are assumed per MURB unit to align with other common Canadian energy modelling assumptions (e.g. EnerGuide)



Base Loads 
*************************

The object key for this section is ``baseLoads``. 

Miscellaneous consumption inputs can be used as a catch-all to indicate any consumption that isn't accounted for by other appliances. Consumption for appliances could be "turned off" by providing an annual consumption value of 0 kWh/y.

  ==================================  ========  ========  =============  ========  ===========  ==========================================================
  Variable Name                       Type      Units     Constraints    Required  Default      Notes
  ==================================  ========  ========  =============  ========  ===========  ==========================================================
  ``clothesWasherConsumption``        double    kWh/y     >=0            No                     Total annual consumption for a clothes washer                                             
  ``dryerConsumption``                double    kWh/y     >=0            No                     Total annual consumption for a dryer                                          
  ``dishwasherConsumption``           double    kWh/y     >=0            No                     Total annual consumption for a dishwasher                                               
  ``refrigeratorConsumption``         double    kWh/y     >=0            No                     Total annual consumption for a refrigerator                                                 
  ``freezerConsumption``              double    kWh/y     >=0            No                     Total annual consumption for a freezer (separate from the primary refrigerator)                                            
  ``dehumidifierConsumption``         double    kWh/y     >=0            No                     Total annual consumption for a dehumidifier                                                 
  ``cookingRangeOvenFuelType``        string              See [#]_       No                     Fuel type for the primary cooking appliance                                                 
  ``cookingRangeOvenConsumption``     double    kWh/y     >=0            No                     Total annual consumption for the primary cooking appliance                                                     
  ``interiorLightingConsumption``     double    kWh/y     >=0            No                     Total annual consumption for all interior lighting                                                   
  ``exteriorLightingConsumption``     double    kWh/y     >=0            No                     Total annual consumption for all exterior lighting                                                    
  ``plugLoadConsumption``             double    kWh/y     >=0            No                     Total annual consumption for all plug loads                                             
  ``miscElectricityConsumption``      double    kWh/y     >=0            No                     Total annual electricity consumption not already accounted for                                                    
  ``miscNaturalGasConsumption``       double    m3/y      >=0            No                     Total annual natural gas consumption not already accounted for                                                
  ``miscPropaneConsumption``          double    L/y       >=0            No                     Total annual propane consumption not already accounted for                                               
  ``miscOilConsumption``              double    L/y       >=0            No                     Total annual oil consumption not already accounted for                                           
  ``miscWoodConsumption``             double    kg/y      >=0            No                     Total annual wood consumption not already accounted for                                               
  ``electricalPanelSize``             double    A         >=0            No                     Electrical panel size                                   
  ==================================  ========  ========  =============  ========  ===========  ==========================================================

  .. [#] ``cookingRangeOvenFuelType`` choices are "electricity", "natural gas", and "propane"


Atypical Loads
*************************

The object key for this section is ``atypicalLoads``. 

Miscellaneous consumption inputs can be used as a catch-all to indicate any consumption that isn't accounted for by other appliances. Consumption for appliances could be "turned off" by providing an annual consumption value of 0 kWh/y.

  ==================================  ========  ========  =============  ========  ===========  ==========================================================
  Variable Name                       Type      Units     Constraints    Required  Default      Notes
  ==================================  ========  ========  =============  ========  ===========  ==========================================================
  ``pool``                            boolean                            No        false        Indicates the presence of an atypical load                                  
  ``poolPump``                        boolean                            No        false        Indicates the presence of an atypical load                                      
  ``poolHeater``                      boolean                            No        false        Indicates the presence of an atypical load                                        
  ``deIcingCables``                   boolean                            No        false        Indicates the presence of an atypical load                                           
  ``extensiveExteriorLighting``       boolean                            No        false        Indicates the presence of an atypical load                                                       
  ``heatedGarage``                    boolean                            No        false        Indicates the presence of an atypical load                                          
  ``hotTub``                          boolean                            No        false        Indicates the presence of an atypical load                                    
  ``mixedUse``                        boolean                            No        false        Indicates whether the building is mixed residential/commercial                                    
  ``outdoorGasAppliance``             boolean                            No        false        Indicates the presence of an atypical load                                                 
  ``swimmingPool``                    boolean                            No        false        Indicates the presence of an atypical load                                          
  ``commonSpaces``                    boolean                            No        false        Indicates the presence of an atypical load                                          
  ``elevator``                        boolean                            No        false        Indicates the presence of an atypical load                                      
  ``fitnessRoom``                     boolean                            No        false        Indicates the presence of an atypical load                                         
  ``snowmeltSystem``                  boolean                            No        false        Indicates the presence of an atypical load                                            
  ==================================  ========  ========  =============  ========  ===========  ==========================================================



Water Usage
*************************

The object key for this section is ``waterUsage``. 


  ==================================  ========  ========  =============  ========  ===========  ==========================================================
  Variable Name                       Type      Units     Constraints    Required  Default      Notes
  ==================================  ========  ========  =============  ========  ===========  ==========================================================
  ``dailyHotWaterConsumption``        double    L/day     >0             No                     The total daily hot water consumption of the entire dwelling                                                                  
  ``dailyTotalWaterConsumption``      double    L/day     >0             No                     The total daily water consumption of the entire dwelling                                                                    
  ==================================  ========  ========  =============  ========  ===========  ==========================================================


Temperature Control
*************************

The object key for this section is ``temperatureControl``. 

  ==================================  ========  ========  =============  ========  ===========  ==========================================================
  Variable Name                       Type      Units     Constraints    Required  Default      Notes
  ==================================  ========  ========  =============  ========  ===========  ==========================================================
  ``hasSmartThermostat``              boolean                            No        false        Indicates the presence of a                                      
  ``smartThermostatModel``            string                             No                     Make/model of smart thermostat                                
  ``heatingSetpointDay``              double    ˚C                       No        22           Heating season daytime set point                                   
  ``heatingSetpointNight``            double    ˚C                       No        22           Heating season nighttime/setback set point                                     
  ``heatingSetbackDuration``          double    hours                    No        0            Heating season setback duration                                        
  ``heatingSetbackStartTime``         double    hours                    No        0            Heating season setback start time (24 hour time, hour starting)                                         
  ``coolingSetpointDay``              double    ˚C                       No        24           Cooling season daytime set point                                     
  ``coolingSetpointNight``            double    ˚C                       No        24           Cooling season nighttime/setback set point                                     
  ``coolingSetbackDuration``          double    hours                    No        0            Cooling season setback duration                                        
  ``coolingSetbackStartTime``         double    hours                    No        0            Cooling season setback start time (24 hour time, hour starting)                                                                                               
  ==================================  ========  ========  =============  ========  ===========  ==========================================================


