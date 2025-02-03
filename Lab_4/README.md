# Olesen-online-GEOG676-spring2025
Dom Olesen GEOG676


import arcpy

arcpy.env.workspace = r'C:\Users\olefi\Desktop\DevSource\GEOG676\Lab4'
folder_path = r'C:\Users\olefi\Desktop\DevSource\GEOG676\Lab4'
gdb_name = 'Lab4.gdb'
gdb_path = folder_path + '\\' + gdb_name

# Create a geodatabase
arcpy.CreateFileGDB_management(folder_path, gdb_name)

# Path to CSV
csv_path = r'C:\Users\olefi\Desktop\DevSource\GEOG676\Lab4\Data\garages.csv'
garage_layer_name = 'Garage_Points'

# Make an XY Event Layer from CSV
garages = arcpy.MakeXYEventLayer_management(csv_path, 'X', 'Y', garage_layer_name)
input_layer = garages
arcpy.FeatureClassToGeodatabase_conversion(input_layer, gdb_path)

# Define path to the newly created feature class
garage_points = gdb_path + '\\' + garage_layer_name

# Open campus gdb and copy buildings feature class
campus = r'C:\Users\olefi\Desktop\DevSource\GEOG676\Lab4\Data\Campus.gdb'
buildings_campus = campus + '\\Structures'  # Path to 'Structures' feature class in Campus.gdb
buildings = gdb_path + '\\Buildings'

# Copy the 'Structures' feature class to the new GDB
arcpy.Copy_management(buildings_campus, buildings)

# Re-Projection - Project the Garage Points
spatial_ref = arcpy.Describe(buildings).spatialReference  # Get spatial reference from buildings
garage_points_reprojected = gdb_path + '\\Garage_Points_reprojected'
arcpy.Project_management(garage_points, garage_points_reprojected, spatial_ref)

# Buffer the garages and Intersect
garageBuffered = arcpy.Buffer_analysis(garage_points_reprojected, gdb_path + '\\Garage_Points_buffered', 150)
arcpy.Intersect_analysis([garageBuffered, buildings], gdb_path + '\\Garage_Building_Intersection', 'ALL')

# Convert the result of the intersection to a CSV
arcpy.TableToTable_conversion(gdb_path + '\\Garage_Building_Intersection.dbf', r'C:\Users\olefi\Desktop\DevSource\GEOG676\Lab4\Data', 'nearbyBuildings.csv')

print("Process completed successfully.")
