# Folder, File, Add Content

The below code is the script to create a directory if does not exist, once the directory is created inside it will create a .txt file with the a specific string and date.

```powershell
# Parameter defined to give a name to the folder we are searching for
param($name_folder)
# Path created to create a new folder in case that we are searching for does not exist 
$Path = "/Users/genaroparedes/Desktop/$name_folder"
"Test to check if path [$Path] exists"
# Check if the folder exist
if (Test-Path -Path $Path) {
    "Path exists!"
} 
# Otherwise create the folder and inside it create a file called created.txt
# and set a content as the following text "This directory was created: "
else {
    "Path doesn't exist."
    "Creating"
    " .
      .
      .
      . "
    $new_path = New-Item -Path "/Users/genaroparedes/Desktop" -Name "$name_folder" -ItemType "directory"
    $date = Write-Output (Get-Date -UFormat "%m/%d/%Y %R")
    Set-Location -Path $new_path
    "This directory was created: " + $date | Out-File -FilePath .\$("Created").txt
    # Here you can put your scripts directory and back to there to continue working
    Set-Location -Path /Users/genaroparedes/Desktop/Powershell-Exercises
}
```

To execute the code shown above just is necessary introduce one parameter, this parameter will the folder name to check if exist or does not. The script will create the specified folder name if does not exist, otherwise just will print "Path exist!"

- For example in the below image, I created a folder called testFolder

![Screen Shot 2021-09-29 at 9.37.08.png](Folder,%20File,%20Add%20Content%20721bb7a4cb514c03bbc3e9c25bddf2f1/Screen_Shot_2021-09-29_at_9.37.08.png)

- If we check the created folder is in desktop path as per defined in my code

![Screen Shot 2021-09-29 at 9.39.48.png](Folder,%20File,%20Add%20Content%20721bb7a4cb514c03bbc3e9c25bddf2f1/Screen_Shot_2021-09-29_at_9.39.48.png)

- Inside of the created folder there is a .txt file, check it out

![Screen Shot 2021-09-29 at 9.42.44.png](Folder,%20File,%20Add%20Content%20721bb7a4cb514c03bbc3e9c25bddf2f1/Screen_Shot_2021-09-29_at_9.42.44.png)

- The .txt mentioned above was filled out with the below text: "This directory was created: 09/29/2021 09:36", the date is the current.

![Screen Shot 2021-09-29 at 9.45.47.png](Folder,%20File,%20Add%20Content%20721bb7a4cb514c03bbc3e9c25bddf2f1/Screen_Shot_2021-09-29_at_9.45.47.png)

# Execution completed!

![Screen Shot 2021-09-29 at 9.47.49.png](Folder,%20File,%20Add%20Content%20721bb7a4cb514c03bbc3e9c25bddf2f1/Screen_Shot_2021-09-29_at_9.47.49.png)