# Olesen-online-GEOG676-spring2025
Dom Olesen GEOG676


import arcpy

#assign bands
source = r"C:\Users\olefi\Desktop\DevSource\GEOG676\Lab7"
band1 = arcpy.sa.Raster(source + r"\band1.TIF") #blue
band2 = arcpy.sa.Raster(source + r"\band2.TIF") #green
band3 = arcpy.sa.Raster(source + r"\band3.TIF") #red
band4 = arcpy.sa.Raster(source + r"\band4.TIF") #NIR
combined = arcpy.CompositeBands_management([band1, band2, band3, band4], source + r"\output_combined.tif")

#Hillshade

azimuth = 315
altitude = 45
shadows = 'NO_SHADOWS'
z_factor = 1 
arcpy.ddd.HillShade(source + r"\DEM.tif.tif", source + r"\output_Hillshade.tif", azimuth, altitude, shadows, z_factor)

#Slope
output_measurement = "DEGREE"
z_factor = 1 
arcpy.ddd.Slope(source + r"\DEM.tif.tif", source + r"\output_slope.tif", output_measurement, z_factor)
print("success!")
