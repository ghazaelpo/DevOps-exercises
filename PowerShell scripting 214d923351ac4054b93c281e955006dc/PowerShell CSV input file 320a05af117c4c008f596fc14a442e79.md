# PowerShell CSV input file

This is the second exercise from PowerShell module:

```powershell
# This script allow you take a csv file and sort by the oldest persons...
# taking a parameter introduced by user to select just the x oldest persons...
# in the csv file
# Then the selected persons are saved in oldestpersons.txt

# Example of how to use the script, you must include the number of persons...
# that you want to save in the oldestpersons.txt
# /path x
# /Users/genaroparedes/Desktop/02-CSV-input-file.ps1 10

param([int]$num) # Declaring the parameter that we will use, you can specify the numbers of persons that you want 
$a = Import-Csv -Path .\csvfile.csv | Sort-Object -Descending Age | Select-Object -First $num # This variable save the sorting and the selection using the parameter $num
$a | Out-File -FilePath .\oldestpersons.txt # Using a pipeline to send $a to Out-File command and create a .txt file
```

For execute this script is mandatory give a parameter to return a file that just include the parameter as you chosen, for example if you put 5 as parameter the file generated just has to include 5 of the oldest people.

![Screen Shot 2021-09-21 at 12.37.24.png](PowerShell%20CSV%20input%20file%20320a05af117c4c008f596fc14a442e79/Screen_Shot_2021-09-21_at_12.37.24.png)