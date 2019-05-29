
### Write to Azure Table Storage using Azure Functions' Output Bindings and Powershell

## Create a new Azure Function App or Powershell

## Create a function

## Add the output binding

## Write some code
Create an array (this array will be sent to Table Storage)
```powershell
$outputArray = @()
```

Using a dictionary to represent each row, add some records to the array. Each row should include the indexes "RowKey" and "PartitionKey". The Partition Key represents the partition in Table Storage where the row will be stored. The RowKey must be a unique value identifying each row within a partition.
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

Associate your array with the output binding
```powershell
Push-OutputBinding -Name outputTable -Value $outputArray
```
