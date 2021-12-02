### Download Ops Agent
https://cloud.google.com/logging/docs/agent/ops-agent/installation#joint-install  
.

### Configuring Ops Agent
https://cloud.google.com/stackdriver/docs/solutions/agents/ops-agent/configuration  
.

### Regex builder
https://regex101.com/  
.

### Powershell script to output the log every 5 seconds.  
Create folder & file first here: `C:\Work\testlog.log`
```PowerShell script:
while(1) { 
$Now = Get-Date 
$Log = "[" + $Now.ToString("yyyy/MM/dd HH:mm:ss.fff") + "]" + " - " + "ERROR" + " - " + "test message"
$LogFile = "C:\Work\testlog.log" 
Write-Output $Log | Out-File -FilePath $LogFile -Encoding Default -append 
Write-Output $Log 
Start-Sleep -Seconds 5 
}
```
.

### config.yaml for Ops Agent.
Location config.yaml `C:\Program Files\Google\Cloud Operations\Ops Agent\config\config.yaml`
```config.yaml
logging:
  receivers:
    saja_test:
      type: files
      include_paths: [c:\Work\testlog.log]
  processors:
    custom_proc:
      type: parse_regex
      field: message
      regex: "^\[(?<time>[^\]]*)\] - (?<severity>[^ ]*) - (?<msg>.*)$"
  service:
    pipelines:
      custom_pipeline:
        receivers: [saja_test]
        processors: [custom_proc]
```
