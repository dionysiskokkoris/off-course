## Config explanation
The following explains what each element of the config JSON file refers to

### Config_example
the config_example.json can be used as template or the config.json

### Locations

The following are locatons for saving files:

|Name|Description|
|---|---|
|ais_path|location of the AIS data|
|cers_path|location of the CERS data|
|ship_class_path|location of the ship class/type data|
|processing_path|location for saving files generated by the code|
|location_path|location for port latitude and longitudes|

### Required files

The following are data files that must be provided in csv format:

|Name|Description|Required columns|Location|Notes|
|---|---|---|---|---|
|ais_filename|data from inside the port|MMSI, dt, lat, long, NavStat, SOG, ROT, COG, HDG|ais_path||
|ais_op_filename1|data from oustide the port|MMSI, dt, lat, long, NavStat, SOG, ROT, COG, HDG|ais_path|in the case felixstowe 4 squares were needed to cover the desired area outside the  port||
|ais_op_filename2|data from oustide the port|MMSI, dt, lat, long, NavStat, SOG, ROT, COG, HDG|ais_path||
|ais_op_filename3|data from oustide the port|MMSI, dt, lat, long, NavStat, SOG, ROT, COG, HDG|ais_path||
|ais_op_filename4|data from oustide the port|MMSI, dt, lat, long, NavStat, SOG, ROT, COG, HDG|ais_path||
|port_filename|data from CERS's port section|?Id, Name, Port Size, Voyage Count|cers_path|These are the default names from the CERS export and are renamed in 1_Data_import|
|vessel_filename|data from CERS's vessel section|?Vessel Id, Vessel Name, Callsign, Gross Tonnage, Last Voyage Id, Last Voyage Created, Last Port of Call, Last Voyage ETA, Last Voyage ETD|cers_path|These are the default names from the CERS export and are renamed in preprocessing/1_Data_import|
|ship_class_filename|data describing the type of each ship|MMSI, Type|ship_class_path||
|cers_eta_filename|data containing the correct ETA for each ship|voyage_id, ETA, etatoportofcall|cers_path|etatoportofcall is the correct ETA|
|weather_data_download_filename|daily weather data used in feature_engineering/2_weather|STN, YEARMODA, TEMP, DEWP, SLP, STP, VISIB, WDSP, MXSPD, MAX, MIN, FRSHTT||downloaded from https://www7.ncdc.noaa.gov/CDO/cdoselect.cmd?datasetabbv=GSOD&countryabbv=&georegionabbv=&resolution=40|
|port_data1|worldwide port locations and names|use default columns from download||downloaded from https://www.unece.org/cefact/codesfortrade/codes_index.html|
|port_data2|worldwide port locations and names|use default columns from download||downloaded from https://www.unece.org/cefact/codesfortrade/codes_index.html|
|port_data3|worldwide port locations and names|use default columns from download||downloaded from https://www.unece.org/cefact/codesfortrade/codes_index.html|
|location_filename|port latitude and longitudes|LOCODE,name,port_size,voyage_count,lat,long|location_path|port data with lats and longs added|
|cers_filename|1 complete year of CERS data|voyage_id, ATA, ATD, ETA, ETD, IMO, in_hazmat, last_port_LOCODE, MMSI, next_port_LOCODE, out_hazmat, POC_LOCODE, vessel_name, voyage_status, Waste Delivery, ETA_year|cers_path|this can be created from the voyage and vessel data|
|voyage files|date from CETS's voyage section|?Voyage ID, Voyage Status, Port of Call LOCODE, Vessel Name, IMO, ETA, ETD ATA, ATD, Last Port LOCODE, Next Port LOCODE, MMSI, In Msg Create Date, Out Msg Create Date, Incoming Hazmat On Board, Outgoing Hazmat On Board|cers_path|it is not necessary to specify the name of each voyage file but they must contain voyage in the filename|

### Generated files

The following are files generated by the code:

|Name|Description|Script|
|---|---|---|
|shipping_filename|AIS and CERS data merged together|Preprocessing/1_Data_import|
|shipping_rot_filename|AIS and CERS data merged together with derived ROT|Preprocessing/2_ROT|
|seg_prep_filename|Sample of MMSI and timestamps with ROT and SOG distributions|Segmentation/1_Segmentation_prep|
|all_segment_variables_filename|All MMSI and time stamps with ROT and SOG distributions|Segmentation/1_Segmentation_prep|
|kmeans_model|k means model used to create segmentation|Segmentation/2_Segmentation|
|segment_filename|All MMSI and time stamps with segments|Segmentation/3_voyage_classification|
|delay_filename|All voyages with a delay flag|feature_engineering/1_Delays|
|weather_data_filename||feature_engineering/2_Weather|
|seasonality_filename||feature_engineering/2_Weather|
|port_loading_filename||feature_engineering/2_Weather|
|port_distance_prep_filename||feature_engineering/2_Weather|
|walking_distance_filename||feature_engineering/2_Weather|
|ship_dynamics_filename||feature_engineering/2_Weather|
|features_filename||feature_engineering/2_Weather|