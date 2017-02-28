# Azure AD Connect Configuration Documenter

AAD Connect configuration documenter is a tool to generate documentation of an Azure AD Connect installation. Currently, the documentation is only limited to the Azure AD Connect sync configuration.

The goal of this project is to:

* To enable quick understanding of the synchronization configuration and "how it happens"!
* To build confidence in getting things right when making changes to the default configuration!!
* To know what was changed when you applied a new build / configuration of Azure AD Connect or added/updated custom sync rules!!!
 
The current capabilities of the tool include:

* Documentation of the complete configuration of Azure AD Connect sync.
* Documentation of any changes in the configuration of two Azure AD Connect sync servers or changes from a given configuration baseline.
* **!!NEW!!** _**Generation of the PowerShell deployment script to migrate the sync rule differences or customisations from one server to another.**_

Prerequisites:

1. .NET Framework 4.5 to be able to run the tool.
2. A modern browser (e.g. Microsoft Edge) to view the report.
3. A fair understanding of MIIS 2003 / ILM 2007 / FIM 2010 / MIM 2016 / AAD Sync sync engine technical concepts to be able to understand the report. A sample report generated by the tool can be found listed in the [Wiki](https://github.com/Microsoft/AADConnectConfigDocumenter/wiki/Sample-Report) section.

How to use the tool:

* Download the latest release AzureADConnectSyncDocumenter.zip from the [releases](https://github.com/Microsoft/AADConnectConfigDocumenter/releases) tab under the Code tab tab, UNBLOCK the downloaded zip file and extract the zip file to an empty local folder on a machine which has .NET Framework 4.5 installed.
	* This will extract the Documenter application binaries along with the sample data files for "Contoso".
	* Make sure that the tool runs by double-clicking on the cmd file AzureADConnectSyncDocumenter.cmd.
* Export the Server Configuration of your pilot / test Azure AD Connect sync server by running Get-ADSyncServerConfiguration cmdlet defined in ADSync module shipped with Azure AD Connect.

```PowerShell

	Import-Module ADSync 
	Get-ADSyncServerConfiguration -Path "<CompletePathToOutputFolder>"

```

* Copy the configuration export files produced in the previous step to a folder under the "Data" directory of the Documenter tool.
	* e.g. the "Pilot" configuration files for the customer "Contoso" are provided as a sample under the "Data\Contoso\Pilot" folder.
* If you want to document the changes from a specific baseline, export the server configuration of your baseline / production Azure AD Connect server and copy the output to a folder under the Documenter "Data" directory.
	* e.g. the "Production" configuration files for the customer "Contoso" are provided as a sample under the "Data\Contoso\Production" folder.
* Edit AzureADConnectSyncDocumenter.cmd for the values of "Pilot" and "Production" directories.
	* If you don't have a baseline / production config, specify the same path as the "Pilot" config.
* Run the updated batch file. Upon successful execution, the generated report will be found in the Documenter "Report" folder. 

**!!Note!!** If the names of the connectors does not exactly match between the supplied "Pilot"  and "Production" configuration files, then before running the batch file, "prep" the exported config files by manually editing the xml files located in the "Connectors" folder so that the name of the connector(s) match. The name of the connector is located inside the "name" element at the start of the content.

A sample report generated by the tool can be found listed in the [Wiki](https://github.com/Microsoft/AADConnectConfigDocumenter/wiki/Sample-Report) section.

[https://aka.ms/aadConnectConfigDocumenter](https://aka.ms/aadconnectconfigdocumenter)

# Code of Conduct

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
