# PSScriptAnalyzer Action

Github action for running PSScriptAnalyzer and use ConvertToSARIF to generate a Static Analysis
Results Interchange Format (SARIF) file. For more information about SARIF, see the
[SARIF website][16].

## Getting Started

To run this action, add the following step to your GitHub Action:

```yaml
- name: Run PSScriptAnalyzer
  uses: microsoft/psscriptanalyzer-action@v1.0
  with:
    path: .\
    recurse: true
    output: results.sarif
```

This YAML code scans all  code in your repository and writes the results to `result.sarif`
in the current working directory.

## YAML

For more info about the inputs, see the [Inputs][01] section of this article.

```yaml
- name: Run PSScriptAnalyzer
  uses: psscriptanalyzer-action
  with:
    path:
    customRulePath:
    recurseCustomRulePath:
    excludeRule:
    includeDefaultRules:
    includeRule:
    severity:
    recurse:
    suppressedOnly:
    fix:
    enableExit:
    settings:
    output:
    ignorePattern:
```

## Inputs

This sections describes the input values used by the action.

The values `output` and `ignorePattern` are action specific. The rest are mapped to the parameters
of `Invoke-ScriptAnalyzer` cmdlet. Every value is of type string.

To provide an array value, enclose the array in single quotes. For example:
`'"value1", "value2", ...'`.

### path

Specifies the path to the scripts or module to be analyzed. Wildcard characters are supported.
Default value is: `.\`. For more information, see the description of the [-Path][08] parameter.

```yaml
with:
  path: .\
```

```yaml
with:
  path: .\src
```

### customRulePath

Specifies the path to the scripts or module to be analyzed. Wildcard characters are supported. For
more information, see the description of the [-CustomRulePath][02] parameter.

```yaml
with:
  customRulePath: '".\customRule.ps1"'
```

```yaml
with:
  customRulePath: '".\customRule.ps1", "customRule2.ps1"'
```

### recurseCustomRulePath

Uses only the custom rules defined in the specified paths to the analysis. To still use the built-in
rules, add the -IncludeDefaultRules switch. For more information, see the description of the
[-RecurseCustomRulePath][10] parameter.

```yaml
with:
  recurseCustomRulePath: true
```

```yaml
with:
  recurseCustomRulePath: false
```

### excludeRule

Omits the specified rules from the Script Analyzer test. Wildcard characters are supported. For more
information, see the description of the [-ExcludeRule][04] parameter.

```yaml
with:
  # exclude one rule
  excludeRule: '"PSAvoidLongLines"'
```

```yaml
with:
  # exclude multiple rules
  excludeRule: '"PSAvoidLongLines", "PSAlignAssignmentStatement"'
```

### includeDefaultRules

Uses only the custom rules defined in the specified paths to the analysis. To still use the built-in
rules, add the -IncludeDefaultRules switch. For more information, see the description of the
[-IncludeDefaultRules][06] parameter.

```yaml
with:
  includeDefaultRules: true
```

```yaml
with:
  includeDefaultRules: false
```

### includeRule

Runs only the specified rules in the Script Analyzer test. For more information, see the description
of the [-IncludeRule][07] parameter.

```yaml
with:
  # Include one rule
  includeRule: '"PSAvoidUsingInvokeExpression"'
```

```yaml
with:
  # Include multiple rules
  includeRule: '"PSAvoidUsingInvokeExpression", "PSAvoidUsingConvertToSecureStringWithPlainText"'
```

### severity

After running Script Analyzer with all rules, this parameter selects rule violations with the
specified severity. For more information, see the description of the [-Severity][12] parameter.

```yaml
with:
  # Report only rule violations with error severity
  severity: '"Error"'
```

```yaml
with:
  # Report only rule violations with error and warning severity
  severity: '"Error", "Warning"'
```

### recurse

Script Analyzer on the files in the Path directory and all subdirectories recursively. For more
information, see the description of the [-Recurse][09] parameter.

```yaml
with:
  recurse: true
```

```yaml
with:
  recurse: false
```

### suppressedOnly

Returns rules that are suppressed, instead of analyzing the files in the path. For more information,
see the description of the [-SuppressedOnly][13] parameter.

```yaml
with:
  suppressedOnly: true
```

```yaml
with:
  suppressedOnly: false
```

### fix

Fixes certain warnings that contain a fix in their **DiagnosticRecord**. For more information, see
the description of the [-Fix][05].

```yaml
with:
  fix: true
```

```yaml
with:
  fix: false
```

### enableExit

Exits PowerShell and returns an exit code equal to the number of error records. For more
information, see the description of the [-EnableExit][03] parameter.

```yaml
with:
  enableExit: true
```

```yaml
with:
  enableExit: false
```

### settings

File path that contains user profile or hash table for ScriptAnalyzer. Does not support passing a
hashtable as an argument. For more information, see the description of the [-Settings][11]
parameter.

```yaml
with:
  settings: .\settings.psd1
```

### output

File path that defines where the SARIF output is written.

```yaml
with:
  output: results.sarif
```

### ignorePattern

Exclude specific files from the SARIF results. Uses regex pattern.

```yaml
with:
  # Any file or folder that have the name test will not be present in the SARIF file.
  ignorePattern: 'tests'
```

## Contributing

This project welcomes contributions and suggestions. Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit <https://cla.opensource.microsoft.com>.

When you submit a pull request, a CLA bot automatically determines whether you need to provide a CLA
and decorates the PR appropriately (for example: status check, comment). Please follow the
instructions provided by the bot. You only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct][14]. For more information see
the [Code of Conduct FAQ][15] or contact [opencode@microsoft.com][18] with any additional questions
or comments.

## Trademarks

This project may contain trademarks or logos for projects, products, or services. Authorized use of
Microsoft trademarks or logos is subject to and must follow
[Microsoft's Trademark & Brand Guidelines][17]. Use of Microsoft trademarks or logos in modified
versions of this project must not cause confusion or imply Microsoft sponsorship. Any use of
third-party trademarks or logos are subject to those third-party's policies.

<!-- link references -->
[01]: #inputs
[02]: https://learn.microsoft.com/powershell/module/psscriptanalyzer/invoke-scriptanalyzer#-customrulepath
[03]: https://learn.microsoft.com/powershell/module/psscriptanalyzer/invoke-scriptanalyzer#-enableexit
[04]: https://learn.microsoft.com/powershell/module/psscriptanalyzer/invoke-scriptanalyzer#-excluderule
[05]: https://learn.microsoft.com/powershell/module/psscriptanalyzer/invoke-scriptanalyzer#-fix
[06]: https://learn.microsoft.com/powershell/module/psscriptanalyzer/invoke-scriptanalyzer#-includedefaultrules
[07]: https://learn.microsoft.com/powershell/module/psscriptanalyzer/invoke-scriptanalyzer#-includerule
[08]: https://learn.microsoft.com/powershell/module/psscriptanalyzer/invoke-scriptanalyzer#-path
[09]: https://learn.microsoft.com/powershell/module/psscriptanalyzer/invoke-scriptanalyzer#-recurse
[10]: https://learn.microsoft.com/powershell/module/psscriptanalyzer/invoke-scriptanalyzer#-recursecustomrulepath
[11]: https://learn.microsoft.com/powershell/module/psscriptanalyzer/invoke-scriptanalyzer#-settings
[12]: https://learn.microsoft.com/powershell/module/psscriptanalyzer/invoke-scriptanalyzer#-severity
[13]: https://learn.microsoft.com/powershell/module/psscriptanalyzer/invoke-scriptanalyzer#-suppressedonly
[14]: https://opensource.microsoft.com/codeofconduct/
[15]: https://opensource.microsoft.com/codeofconduct/faq/
[16]: https://sarifweb.azurewebsites.net/
[17]: https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general
[18]: mailto:opencode@microsoft.com
