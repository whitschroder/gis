# Software

## ArcGIS Pro

ArcGIS Pro is available for download from the UF Geoplan Center [here](https://www.geoplan.ufl.edu/software/arcgis-pro/). You will need to be on the UF network or use the [Gatorlink VPN](https://it.ufl.edu/get-help/infrastructure/network-infrastructure/vpn/). When downloading the installation file, select the most recent version. Open the installation file and complete the installation steps using the default settings. During the installation, you may be prompted to update Microsoft .NET Desktop Runtime. Click on the link provided in the pop-up window, and download the specific version listed (currently version 10.0, x64). Once you open ArcGIS Pro after installation, you might be prompted to install an update. Click on the link and follow the installation process again.

## Bootcamp

For Mac users, ArcGIS Pro can be run through a Windows partition (e.g. Bootcamp) with an additional purchase of Windows. Additional information is available [here](https://pro.arcgis.com/en/pro-app/latest/get-started/run-pro-on-a-mac.htm).

## UF Apps

For Mac and Windows users, ArcGIS Pro can be run through [UF Apps](https://info.apps.ufl.edu/). Login to UF Apps and select either the Native Client or the HTML access. If you choose the former, you will have to download and install the Horizon Client. If using the HTML access, select UFApps Graphics. To open ArcGIS Pro on UF Apps, click the Windows button at the bottom center and search for ArcGIS Pro, then open. When prompted with the ArcGIS Sign In window, choose the "Your ArcGIS organization's URL option." Type ufl in the box (the full url should be ufl.maps.arcgis.com). Click Continue. To manage files, you will have to use the M Drive, accessible from the virtual desktop. To upload files to the M Drive, click on the side bar to the left, and the Open File Transfer panel at the top of the side bar. Click Upload, and Choose Files. To download files to your computer from the M Drive, click Download, then open a new window with your M Drive, navigate to the file you want to transfer, select it, and click CTRL + C or COMMAND + C. The file should appear in the File Transfer panel, click the download arrow, and select the download location. Transferring files is easier with the Horizon Client. Open the M Drive in the Horizon Client and open a separate file folder on your local computer. Highlight and drag the files from your local computer to the M Drive.

## QGIS

For Windows or Mac users, QGIS is a good alternative to ArcGIS Pro. QGIS can be downloaded for free [here](https://qgis.org/download/). Select the long-term version based on your platform. Once downloaded, run the installer with default settings. QGIS includes several in house tools, but additional plugins are available under Plugins -> Manage and Install Plugins.

## SAGA

SAGA is a GIS software that was previously integrated with QGIS. If using QGIS on Windows, SAGA is still available by installing the Processing Saga NextGen Provider, available under Plugins -> Manage and Install Plugins. Then in QGIS go to Settings -> Options -> Processing, and under Providers and SAGANG, choose the SAGA folder where SAGA is installed. In Windows, the folder should be something like C:\Program Files\QGIS 3.44.12\apps\saga, but this will depend on your specific QGIS installation.

If using QGIS on a Mac, you will need to install SAGA separately [here](https://sourceforge.net/projects/saga-gis). Once installed, open the zip file and copy the SAGA application to Applications. The Processing Saga NextGen Provider plugin is not available in QGIS on a Mac. However, you can run SAGA as a standalone interface. To use SAGA, you have to open your input file by clicking the folder icon at top left. Then under tools, select the appropriate tool. You can also search for the tool by name by clicking the gear icon. In the search box, type the name of the tool, click anywhere, then click Okay. When running each tool, you have to provide the name of the input file (which first has to be opened with the folder icon). Next to any outputs, select <create>. Then select any parameters under Options. Click Okay to run the tool. The output if successful, will be available under Data at the top left. Click the data and then click the save icon to export the file (change file type to GeoTIFF). This file can then be loaded into QGIS.

## GRASS

In Windows, GRASS should be automatically included in QGIS. You may need to install or activate (clicking the check box) the GRASS Processing Provider from Plugins -> Manage and Install Plugins.

On a Mac, you will need to install GRASS separately [here](https://grass.osgeo.org/download/mac). Install GRASS 8.4.2 (legacy) based on your operating system. Once installed, copy GRASS to your Applications.

To activate GRASS in QGIS, go to Settings -> Options, click on System, and under Environment, check the box next to Use custom variables. Click the plus sign to add variables. You will need to add the following three variables:

| Apply | Variable | Value |
| --- | --- | --- |
| Prepend | GRASS_PREFIX | /Applications/GRASS-8.4.app/Contents/Resources |
| Prepend | GISBASE | /Applications/GRASS-8.4.app/Contents/Resources |
| Prepend | PROJ_NETWORK | ON |

Then click OK. Restart QGIS, and you should now see the GRASS tools in the Processing Toolbox.

If GRASS is not working in QGIS, GRASS can be opened as its own standalone software similar to SAGA.

## Whitebox Workflows

To use Whitebox Workflows in QGIS, go to Plugins -> Manage and Install Plugins, search for Whitebox Workflows for QGIS, and install. You may need to restart QGIS after installing the plugin. Next go to Plugins -> Whitebox Workflows -> Check Backend Updates. Currently, the installation of backend updates is leading to errors on some devices.
