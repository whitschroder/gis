# Software

## ArcGIS Pro

ArcGIS Pro is available for download from the UF Geoplan Center [here](https://www.geoplan.ufl.edu/software/arcgis-pro/). You will need to be on the UF network or use the [Gatorlink VPN](https://it.ufl.edu/get-help/infrastructure/network-infrastructure/vpn/). When downloading the installation file, select the most recent version. Open the installation file and complete the installation steps using the default settings. During the installation, you may be prompted to update Microsoft .NET Desktop Runtime. Click on the link provided in the pop-up window, and download the specific version listed (currently version 10.0, x64). Once you open ArcGIS Pro after installation, you might be prompted to install an update. Click on the link and follow the installation process again.

## Bootcamp

For Mac users, ArcGIS Pro can be run through a Windows partition (e.g. Bootcamp) with an additional purchase of Windows. Additional information is available [here](https://pro.arcgis.com/en/pro-app/latest/get-started/run-pro-on-a-mac.htm).

## UF Apps

For Mac and Windows users, ArcGIS Pro can be run through [UF Apps](https://info.apps.ufl.edu/). Login to UF Apps and select either the Native Client or the HTML access. If you choose the former, you will have to download and install the Horizon Client. If using the HTML access, select UFApps Graphics. To open ArcGIS Pro on UF Apps, click the Windows button at the bottom center and search for ArcGIS Pro, then open. When prompted with the ArcGIS Sign In window, choose the "Your ArcGIS organization's URL option." Type ufl in the box (the full url should be ufl.maps.arcgis.com). Click Continue. To manage files, you will have to use the M Drive, accessible from the virtual desktop. To upload files to the M Drive, click on the side bar to the left, and the Open File Transfer panel at the top of the side bar. Click Upload, and Choose Files. To download files to your computer from the M Drive, click Download, then open a new window with your M Drive, navigate to the file you want to transfer, select it, and click CTRL + C or COMMAND + C. The file should appear in the File Transfer panel, click the download arrow, and select the download location. Transferring files is easier with the Horizon Client. Open the M Drive in the Horizon Client and open a separate file folder on your local computer. Highlight and drag the files from your local computer to the M Drive.

## QGIS

For Windows or Mac users, QGIS is a good alternative to ArcGIS Pro. QGIS can be downloaded for free [here](https://qgis.org/download/). Select the long-term version based on your platform. Once downloaded, run the installer with default settings.

## SAGA

If using QGIS, you will also want to install SAGA, which can be used through the QGIS interface. If using Windows, SAGA should already be installed. To use SAGA, in QGIS go to Settings -> Options -> Processing, and under Providers and SAGANG, choose the SAGA folder where SAGA is installed. In Windows, the folder should be something like C:\Program Files\QGIS 3.44.12\apps\saga.

If using QGIS on a Mac, you may need to install SAGA separately [here](https://sourceforge.net/projects/saga-gis). Once installed, in QGIS go to Settings -> Options -> Processing, and under Providers and SAGANG, choose the SAGA folder where SAGA is installed. On a Mac, the folder should be something like /Applications/SAGA.app/Contents/MacOS.

## Whitebox Workflows

To use Whitebox Workflows in QGIS, go to Plugins -> Manage and Install Plugins, search for Whitebox Workflows for QGIS, and install. You may need to restart QGIS after installing the plugin. Next go to Plugins -> Whitebox Workflows -> Check Backend Updates.

## GRASS

In Windows, GRASS should be automatically included in QGIS. You may need to install or activate the GRASS Processing Provider from Plugins -> Manage and Install Plugins.

On a Mac, you will need to install GRASS separately [here](https://grass.osgeo.org/download/mac). Then update the GRASS location in QGIS under Settings -> Options -> Processing, Providers and GRASS. The location on a Mac should be something like /Applications/GRASS-X.X.app/Contents/Resources, where X.X is the GRASS version.

Recently GRASS has not been working in QGIS on a Mac. If GRASS is not working in QGIS, GRASS can be opened as its own standalone software.
