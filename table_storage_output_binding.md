
### Write to Azure Table Storage using Azure Functions' Output Bindings and Powershell

## Create a new Azure Function App for Powershell

Add a new Function App, specifying the "Powershell (Preview)" Runtime Stack:
![New Function App](images/newfunctionapp.png)

## Create a function
There are a few steps to create a new function, here's the abridged version.

Push the "+" button next to the "Functions" section of your new Function App, and then select "HTTP Trigger" as the trigger type:
![New Function App](images/newfunction1.png)

Choose a name for the function:
![New Function App](images/newfunction2.png)

The sample code should now appear:
![New Function App](images/newfunction2.png)

## Add the output binding

## Write some code

Create an array (this array will be sent to Table Storage):
```powershell
$outputArray = @()
```

Using a dictionary to represent each row, add some records to the array. Each row should include the indexes "RowKey" and "PartitionKey". The Partition Key represents the partition in Table Storage where the row will be stored. The RowKey must be a unique value identifying each row within a partition:
```powershell
while($val -ne 10)
     {
       $outputRow = @{}
       
       $outputRow["PartitionKey"] = "MyPartition"
       
       ##This value must be unique within each partition. If it is not, the existing row will be overwritten!
       $outputRow["RowKey"] = $val
       
       ##Add the row to the output array
       $outputArray += $outputRow
       
       $val++
     }
```

Associate your array with the output binding:
```powershell
Push-OutputBinding -Name outputTable -Value $outputArray
```
