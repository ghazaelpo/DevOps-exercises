# PowerShell scripting

# Hello World

This is the first exercise from PowerShell module:

```powershell
# Script to take two parameters, the first parameter...
# will use as the name that you want give to your file "Hello-your name"
# The second parameter is a string and this will include into the text file with the generated random number
# that is created

# Example of how to use the script, you must include the path and both parameters
# /path $param1 $param2
# /Users/genaroparedes/Desktop/01-Hello-World.ps1 Genaro "This is a random number"

param ($param1,[string]$param2) # Declaring two parameters to proceed to use them, $param1 to create our name file and $param2 to add the text from this into the file that we will create
$random = Get-Random | Write-Output # This variable save a random number
Write-Output ($param2 + ': ' + $random | Out-File -FilePath .\$("Hello-" + $param1).txt) # Write-Output command write your $param2 into the .txt file and Out-File create the file and take $param1 to give a name
```

As you can see, to execute this script we must include the path and then the two parameters, in this example the first parameter is my name because I want that my generated file has the name "Hello-Genaro.txt" and second parameter is a string, whatever you want, in my case I chosen "This is a random number" because the file has within it a random number, so the output will "This is a random number: 202528763".

![Screen Shot 2021-09-21 at 11.30.55.png](PowerShell%20scripting%20214d923351ac4054b93c281e955006dc/Screen_Shot_2021-09-21_at_11.30.55.png)

You can choose different parameters as shown in the below example:

In this case I selected Erick as first parameter, so the file name is "Hello-Erick.txt" and as second parameter I typed "here you are a random number".

![Screen Shot 2021-09-21 at 11.48.22.png](PowerShell%20scripting%20214d923351ac4054b93c281e955006dc/Screen_Shot_2021-09-21_at_11.48.22.png)

[PowerShell CSV input file](PowerShell%20scripting%20214d923351ac4054b93c281e955006dc/PowerShell%20CSV%20input%20file%20320a05af117c4c008f596fc14a442e79.md)