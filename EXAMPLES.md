powershell.ps1  

might need a bit of cleanup, but i'll do later.. because learned rust while making this fork in a way...  
```
function swscli ($filename)
{
	$file = Get-Item $filename;
    $fileName = Get-Item $filename
	$filetxtname = $($fileName.Name)
	
    $uri = "http://my-simpler-srv.local:8000/"
    
    $currentPath = Convert-Path .
    $filePath="$currentPath\$fileName"
    
    $fileBin = Get-Content -Path $fileName.FullName -Raw
    $boundary = [System.Guid]::NewGuid().ToString()
    $LF = "`r`n"
    $bodyLines = (
        "--$boundary",
        "Content-Disposition: form-data; name=`"files`"; filename=`"$filetxtname`"; csrf=`"notoken`"",
        "Content-Type: application/octet-stream$LF",
        $fileBin,
        "--$boundary--$LF"
    ) -join $LF
    
    $headers = @{
        "Content-Type" = "multipart/form-data; boundary=`"$boundary`""
    }
    
    Invoke-RestMethod -Uri $uri -Method POST -Headers $headers -Body $bodyLines
}

function transfersh ($filename)
{
  $file = Get-Item $filename;
  (Invoke-WebRequest -Method POST -InFile $file.FullName -Uri http://comapredwith.transfer.sh:8000/$($file.Name)).Content
}

# Example usage
swscli(".\my-automatic-output.csv")
```

If CURL is available on Windows (should be by default in W10 and W11 unless your workplace blocks it), and Linux distros
curl.exe -v -X POST -F "csrf=notoken" -F "files=@$MyFile.csv;filename=$MyFile.csv" http://my-simpler-srv.local:8000/