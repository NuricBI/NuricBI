## DATA MODEL CLEANER FOR POWER BI AND ANALYSIS SERVICES (SSAS)

This is the first version of a tool I created to help you in the process of clean your data models, which can become a nightmare if you don’t have an effective and fast way to do it.

### Challenge
When developers remove unnecessary objects from large data models, connected reports break a and the validation process is manual, tedious and time-consuming.

### Solution
When I tried to clean my data models I couldn’t find any tool with all the functionalities I needed, so decided to create my own using Power BI, which allows:

– Obtain all the dependencies of the data model in an efficient and automated way.

– Identify the list of objects (measures, columns, calculated columns, tables) in use and those that are not, in the reports connected to the Power BI or SSAS Data model.

I hope it can help you in the process of keeping your data models optimized 😊.

### How It Works

1. Get the dependencies between all objects in the data model: This tool identifies how all the objects in your data model are connected to each other. For example, if you want to remove a measure, you will be able to detect the impact on your reports.

To get the dependencies I used Dynamic Management Views (DMV) which are queries that return information about model objects, server operations and server status. If you want to know more that DMVs, check our article What are Dynamic Management Views (DMVs) and what are they for?.

The main DMV that I used is the DISCOVER_CALC_DEPENDENCY, which Returns information about the calculation dependency for an object that is specified in a Tabular database or in a DAX query that is executed against a Tabular database.

2. Identify the objects used in the data model: For that I used the tool “Report Analyzer” explained in detail in this article: Report Analyzer

Finally, I related the information provided for the DMVs and I merged it with the information generated for the Report Analyzer in a Power BI report.

### How to Use the Tool

You can use this tool in any Power BI data model with the following simple steps:

1. Get the connection details of a Power BI Dataset

Local Power BI Dataset:

Open a Power BI Dataset that you want to document. Open DAX Studio and choose the “PBI / SSDT Model” data source option, then click on Connect:

![Connection](https://user-images.githubusercontent.com/47791555/196967326-8300fdb4-52a7-4b29-8ffc-f96fb81e6ab1.jpg)

In the lower right-hand corner of the screen is the name of the server, and the port number you have connected to. In this case it is localhost:52223

![Server](https://user-images.githubusercontent.com/47791555/196967493-816abcd3-8df6-4e79-8f8a-98228e1f45ae.png)

Run the following DMV query in a DAX query window. This will give you the GUID, the name of the only database in the Power BI data model:

SELECT [CATALOG_NAME] FROM $SYSTEM.DBSCHEMA_CATALOGS

![DB](https://user-images.githubusercontent.com/47791555/196967592-2773c6e6-3762-40d6-9966-1371d5e2ee01.png)

Power BI Premium

– Server: Go to “Workspace settings” and copy the Workspace Connection.

![workspace connection](https://user-images.githubusercontent.com/47791555/196967690-dd5f9f2c-b076-4997-a035-61b88f14904c.jpg)

– Database: Is the dataset name.

2. Update the Dataset parameters in the Data model cleaner tool:

![parameters](https://user-images.githubusercontent.com/47791555/196968523-a53da5d3-e7fe-402a-b888-2300845a5333.jpg)

3. Get all the objects used in the Power BI reports connected to the data model:

– Save all the PBI report files connected to the golden dataset in a folder.

– Open External tool: Report Analyzer:

![Performance Analyzer](https://user-images.githubusercontent.com/47791555/196967905-f6b28cfe-fabf-45bb-a3fa-2d02e246d347.jpg)

– Click on “Select folder”:

![Performance Analyzer 2](https://user-images.githubusercontent.com/47791555/196968054-5d42aba9-76a4-4857-81cb-af324eef2bab.jpg)

– Select the respective folder, and select “Export Report Metadata”:

![Performance Analyzer 3](https://user-images.githubusercontent.com/47791555/196968151-dbcc1986-8710-43df-918f-4f2de11cd326.jpg)

– You will see the following message:

![message](https://user-images.githubusercontent.com/47791555/196968245-c293310f-df20-4eff-b9a2-d70957afcfc4.jpg)

The files in .txt format will be saved in the same folder where the reports are.

4. Update the “LocalSoucePBITemplates” parameter in Power BI:

Type the location of the folder with the .txt files generated by the Report Analyzer:

![Edit parameters](https://user-images.githubusercontent.com/47791555/196968338-81dc322b-5d13-4007-acf5-40183e559aa6.jpg)

Information provided by the Data Model Cleaner tool

– Object dependencies: On this tab you can consult the list of calculated objects affected by the selected object:

![dependencies](https://user-images.githubusercontent.com/47791555/196968639-32713f21-1e84-43c0-9beb-27f7ec4998e3.jpg)

– Calculated Objects Breakdown: This tab shows the breakdown of the queried calculated object.

![Breakdown](https://user-images.githubusercontent.com/47791555/196968746-c1f23a6d-fb0f-48d5-93f9-4704d26fb061.jpg)

– Objects Used / Unused List: On this tab you can easily consult the Used / Unused list of the objects that will help you make decisions about hiding or removing them from the model.

If you consult by table additionally you will see the “M” or DAX expression of the table.

To determine the used list of objects this tool consider:

- Visuals and custom visuals
- Report-Level measures
- Filters added to the visuals, pages, and reports
- Bookmarks

![used unused objects](https://user-images.githubusercontent.com/47791555/196968828-ea037bd1-5e64-4680-b5b6-b0f1997d0cd9.jpg)

You can also drill through on any object used and consult the reports, pages and in which of the visualizations this object is being used:

![drill menu](https://user-images.githubusercontent.com/47791555/196968929-287849db-069d-489d-9b2b-ecf0b07f45b5.jpg)

![drill](https://user-images.githubusercontent.com/47791555/196969281-8bafcbb2-408c-4d0c-afe2-1e13181000d8.jpg)

– Used Objects in the Reports: List of objects used by report.

![used objects](https://user-images.githubusercontent.com/47791555/196969052-2e7bb2d3-fbb4-4908-a5c0-5039136e6018.jpg)

### Download Tabular Model Cleaner tool here 👇:
[Tabular Model Cleaner tool.zip](https://github.com/NuricBI/NuricBI/files/9830843/Tabular.Model.Cleaner.tool.zip)

### Download Essential Checklist to Keep your Power BI Solutions Optimized here 👇:
[Essential Checklist to Keep your Power BI Solutions Optimized.xlsx](https://github.com/NuricBI/NuricBI/files/9831560/Essential.Checklist.to.Keep.your.Power.BI.Solutions.Optimized.xlsx)


