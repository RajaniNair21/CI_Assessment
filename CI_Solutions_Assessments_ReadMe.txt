Note on github upload:

The packages folder under the UI project was large(125 MB), which prevented me from uploading the same. I have zipped each folder (CI_Solutions.zip, DAL.zip, Rest_API.zip) which are all part of the CI_Solutions.sln file.

1) The Hierarchical Data Viewer UI has been implemented with required controls. For now, dummy data from a sample json file is used to load data into the listview.

When trying to fetch the hierarchical data from the DB (and call it from the REST API (which talks to the DAL), I faced the issue as described below:

Attempted to write a recursive CTE (which would be wrapped inside an SP, so it could be invoked through the EF and therefore by the REST API, since RestAPI does not support CTEs). (Have included the CTEs under the folder 'DB Scripts').The CTE written either did not result the hierarchical data OR went into an infinite loop.
Hence, opted to load some dummy data into the UI.

2) Radio button toggle(Part Number/File Name) should ideally load the corresponding data(PartNumber/FileName) into the 'ItemName' column. However, despite using an observable collection (so UI is automatically updated when the underlying data source is changed), the default collection is being loaded, though the underlying collection doe have the corresponding elements. This is a binding issue. 

3) The RestAPI url needs to be changed(in Constants.cs) to the corresponding local url on your machine, when running the application.

4) The BOMController class inside the RestAPI project, includes a GetConfigurationsByPartNumber, which for testing purpose includes a GROUP join query so the resulting JSON can be returned to the UI. This needs to be replaced with the SP call as mentioned in point 1 above.

5) Displaying ItemName column contents as a treeview is in progress.

