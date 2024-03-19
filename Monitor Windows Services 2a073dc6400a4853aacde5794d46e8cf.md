# Monitor Windows Services

The below code is the script created to print an alert if one of the services is stopped, it show if the service is running as well.

```powershell
# Created variable to save default services as per requested
# We can stop any of these services to see how the script works
$services = "wuauserv", "WSearch", "Themes"

# Iterate the variable $service in $services to get service by service
# Then check every service from $service variable
foreach($service in $services){
  # check the status of the service 
  $service_status = (Get-Service -Name $service).status
  # Print status service, running or stopped
  Write-Host ($service +": "+ $service_status)
  # If service does not run
  if(!($service_status -eq "Running")){
    Write-Host "Service stopped, try using Start-Service -Name $service" 
  }
}
```

### Let me show you how it works:

- If we execute the script without stopping any service, the output will be the running services

```powershell
PS C:\Users\hazae\Desktop> .\03-Monitor-Windows-Services.ps1
wuauserv: Running
WSearch: Running
Themes: Running
```

![Untitled](Monitor%20Windows%20Services%202a073dc6400a4853aacde5794d46e8cf/Untitled.png)

- In this example I stopped "wuauserv" service to see how the script works

```powershell
PS C:\Users\hazae\Desktop> Stop-Service -Name "wuauserv"
PS C:\Users\hazae\Desktop> .\03-Monitor-Windows-Services.ps1
wuauserv: Stopped
Service stopped, try using Start-Service -Name wuauserv
WSearch: Running
Themes: Running
```

![Untitled](Monitor%20Windows%20Services%202a073dc6400a4853aacde5794d46e8cf/Untitled%201.png)

- If we stopped all the services, the output is the below:

```powershell
PS C:\Users\hazae\Desktop> Stop-Service -Name "Themes"
PS C:\Users\hazae\Desktop> .\03-Monitor-Windows-Services.ps1
wuauserv: Stopped
Service stopped, try using Start-Service -Name wuauserv
WSearch: Running
Themes: Stopped
Service stopped, try using Start-Service -Name Themes
PS C:\Users\hazae\Desktop> Stop-Service -Name "WSearch"
PS C:\Users\hazae\Desktop> .\03-Monitor-Windows-Services.ps1
wuauserv: Stopped
Service stopped, try using Start-Service -Name wuauserv
WSearch: Stopped
Service stopped, try using Start-Service -Name WSearch
Themes: Stopped
Service stopped, try using Start-Service -Name Themes
```

![Untitled](Monitor%20Windows%20Services%202a073dc6400a4853aacde5794d46e8cf/Untitled%202.png)

- Finally run again all the services

```powershell
PS C:\Users\hazae\Desktop> Start-Service -Name "WSearch"
PS C:\Users\hazae\Desktop> Start-Service -Name "Themes"
PS C:\Users\hazae\Desktop> Start-Service -Name "wuauserv"
PS C:\Users\hazae\Desktop> .\03-Monitor-Windows-Services.ps1
wuauserv: Running
WSearch: Running
Themes: Running
PS C:\Users\hazae\Desktop>
```

![Untitled](Monitor%20Windows%20Services%202a073dc6400a4853aacde5794d46e8cf/Untitled%203.png)

[Folder, File, Add Content](Monitor%20Windows%20Services%202a073dc6400a4853aacde5794d46e8cf/Folder,%20File,%20Add%20Content%20721bb7a4cb514c03bbc3e9c25bddf2f1.md)