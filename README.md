# hyper_v_gpu_passthrough
Passthrough gpu support to hyper-v virtual machine.
## how to run
```
powershell .\gpu_passthrough.ps1 vm_name
```

## dll migration
On your host machine, go to `C:\Windows\System32\DriverStore\FileRepository\`
and copy the `nv_dispi.inf_amd64` folder to `C:\Windows\System32\HostDriverStore\FileRepository\` on your VM (This folder will not exist, so make sure to create it)
Next you will need to copy `C:\Windows\System32\nvapi64.dll` file from your host to `C:\Windows\System32\` on your VM
And once that is done, you can restart the VM.

## Restore VMGpuPartitionAdapter
```batch
Remove-VMGpuPartitionAdapter -VMName $yourvmname -ErrorAction SilentlyContinue
```
## Restore EnhancedSessionMode
```batch
Set-VMHost -EnableEnhancedSessionMode $True
```

## if failed to run script, try running
```
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```
or this
```
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```


## About the slowdown of the Hyper-V virtual machine network
The host computer is connected to the WIFI network. I tried to change the adapter option in the network and Internet to find the WLAN (this is if the name is not changed), right-click to open the properties, find the configuration under the network card name, select the advanced tab, find the preferred frequency band and change it to the preferred 5GHz/6Ghz frequency band. save.

# reference
https://www.reddit.com/r/sysadmin/comments/jym8xz/gpu_partitioning_is_finally_possible_in_hyperv/

