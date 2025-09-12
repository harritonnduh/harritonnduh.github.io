# HARRITON NDUH

## Introduction to Autorun

used for getting an extremely comprehensive view of startup applications, services, executables, etc trhroughout the whole system. provides a GUI and CLI option. isn't really specialized for creating and comparing baselines. but an extended 

### Autorun Baseline Creation and Comparison in Windows using "Autoruns" from [P0w3rsh3ll](https://github.com/p0w3rsh3ll/AutoRuns)

The tool is just an open source take on [Autorun](#Autorun), but doens't use its actual code. It is a poweshell script and specializes in the creation of baselines and incidence response.

it can be imported from [here](https://github.com/p0w3rsh3ll/AutoRuns/blob/master/AutoRuns.psm1) using the `import-module` command in powershell after downloading. You can verify the module has been impored with the `get-module` command, and see its available commands with the `get-command -module autorun` command (looks for commands found in the autorun module)

To run a baseline, use the following commands (multiline)

``` powershell
Get-PSAutorun -VerifyDigitalSignature |
Where { -not($_.isOSbinary)} |
New-AutoRunsBaseLine -Verbose -filepath ./baseline-scan.ps1
```

> dont know wtf the first two lines do but
> -filepath = specifies the location and name of the created baseline file

When one wants to scan the system and compare with the baseline, run the same set of commands and store output to a different file

``` powershell
Get-PSAutorun -VerifyDigitalSignature |
Where { -not($_.isOSbinary)} |
New-AutoRunsBaseLine -Verbose -filepath ./current-scan.ps1
```

Now compare the two scans, and the output would show the anomalies which are in this case the applications, services, exectuables, etc that have been configured eitehr maliciuosly or not to run on startup/logon, which were not during the creation of the baseline.

```powershell
Compare-AutoRunsBaseLine -ReferenceBaseLineFile ./baseline-scan.ps1 -DifferenceBaseLineFile ./current-scan.ps1
```
