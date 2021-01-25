# ufs-land-driver

ufs-land-driver: a simple land driver for the UFS land models

<pre>This is a primary tree starting at the program 'ufsLandDriver'

ufsLandDriver
+-ufsLandNoahMPDriverInit-+-static%ReadStatic(read in dimension length for location and soil_levels,
|                         |                   read in latitude,longitude,vegetation_category,
|                         |                   soil_category,slope_category,deep_soil_temperature,
|                         |                   elevation,land_mask,soil_level_thickness,
|                         |                   soil_level_nodes,max_snow_albedo,emissivity,
|                         |                   gvf_monthly,albedo_monthly,lai_monthly,z0_monthly,
|                         |                   iswater,isice,isurban,land_cover_source,
|                         |                   soil_class_source)
|                         +-noahmp%Init(memory allocation and assignment of default values)
|                         +-initial%ReadInitial(read in dimension length for location and
|                         |                     soil_levels, read in time,date,latitude,longitude,
|                         |                     snow_water_equivalent,snow_depth,canopy_water,
|                         |                     skin_temperature,soil_level_thickness,
|                         |                     soil_level_nodes,soil_temperature,soil_moisture,
|                         |                     soil_liquid,iswater,isice,isurban,
|                         |                     land_cover_source)
|                         +-initial%TransferInitialNoahMP
|                         +-static%TransferStaticNoahMP
|                         +-noahmp%TransferNamelist
|                         +-forcing%ReadForcingInit(read in dimension length of location and time,
|                                                   read in time, memory allocation for temperature,
|                                                   specific_humidity,surface_pressure,wind_speed,
|                                                   downward_longwave,downward_shortwave,
|                                                   precipitation)
+-ufsLandNoahMPDriverRun-+-set_soilveg
|                        +-gpvs
|                        +-date_from_since
|                        +-noahmp%InitStates (called for the first timestep)
|                        +-forcing%ReadForcing (read in time,temperature,specific_humidity,
|                        |                      surface_pressure,wind_speed,downward_longwave,
|                        |                      downward_shortwave,precipitation)
|                        +-interpolate_monthly-+-date_from_since
|                        |                     +-calc_sec_since
|                        +-calc_cosine_zenith-+-date_from_since
|                        |                    +-calc_sec_since
|                        +-noahmpdrv_run-+-NOAHMP_SFLX-+-ATM(re-process atmospheric forcing)
|                        |                             +-PHENOLOGY(vegetation phenology considering
|                        |                             |           vegeation canopy being buries by
|                        |                             |           snow and evolution in time)
|                        |                             +-PRECIP_HEAT
|                        |                             +-ENERGY-+-THERMOPROP-+-CSNOW
|                        |                             |        |            +-TDFCND
|                        |                             |        +-RADIATION-+-ALBEDO-+-SNOW_AGE
|                        |                             |        |           |        +-SNOWALB_BATS
|                        |                             |        |           |        +-SNOWALB_CLASS
|                        |                             |        |           |        +-GROUNDALB
|                        |                             |        |           |        +-TWOSTREAM
|                        |                             |        |           +-SURRAD
|                        |                             |        +-VEGE_FLUX-+-SFCDIF1
|                        |                             |        |           +-SFCDIF2
|                        |                             |        |           +-STOMATA
|                        |                             |        |           +-CANRES
|                        |                             |        |           +-ESAT
|                        |                             |        |           +-RAGRB
|                        |                             |        +-BARE_FLUX
|                        |                             |        +-TSNOSOI-+-HRT
|                        |                             |        |         +-HSTEP-+-ROSR12
|                        |                             |        +-PHASECHANGE-+-FRH2O
|                        |                             +-WATER-+-CANWATER
|                        |                             |       +-SNOWWATER-+-SNOWFALL
|                        |                             |       |           +-COMBINE
|                        |                             |       |           +-DIVIDE-+-COMBO
|                        |                             |       |           +-COMPACT
|                        |                             |       |           +-SNOWH2O
|                        |                             |       +-SOILWATER-+-ZWTEQ
|                        |                             |       |           +-INFIL
|                        |                             |       |           +-SRT-+-WDFCND1
|                        |                             |       |           |     +-WDFCND2
|                        |                             |       |           +-SSTEP
|                        |                             |       +-GROUNDWATER
|                        |                             |       +-SHALLOWWATERTABLE
|                        |                             +-CARBON-+-CO2FLUX
|                        +-WriteOutputNoahMP
+-ufsLandNoahMPDriverFinalize</pre>
