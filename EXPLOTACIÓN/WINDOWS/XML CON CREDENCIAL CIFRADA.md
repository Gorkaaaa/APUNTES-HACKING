```shell
powershell -c "$cred = Import-CliXml -Path cred.xml; $cred.getNetworkCredential() | Format-List *"
```