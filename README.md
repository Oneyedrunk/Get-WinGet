# <img src="Windows.svg" alt="Windows 11" width="26"/> WinGet Cheat Sheet

### Query Options
> Used to search for packages or narrow down search results / list outputs.

| _--query \ -q_ |                                        | _--query \ -q_ |                                    |
| -------------- | -------------------------------------- | -------------- | ---------------------------------- |
| --id           | winget update --id _Mozilla.Firefox_   | --source \ -s  | winget list --source _winget_      |
| --name         | winget find --name "_Visual Studio_"   | --tag          | winget search --tag _vscode_       |
| --version \ -v | winget remove _powershell_ -v _0.15.2_ | --exact \ -e   | Use the exact string of the query. |
>### **Tip:**  
> Use `--help` or `-?` with any command for more information: `winget <command> --help`
### List \ Search \ Show

| _WinGet list_       |                             | _WinGet search {package}_             | _WinGet show {package}_               |
| ------------------- | --------------------------- | ------------------------------------- | ------------------------------------- |
| **Alias**: _ls_     | List installed packages     | **Alias**: _find_                     | **Alias**: _view_                     |
| --count \ -n _10_   | Limit to _10_ results       | Search available packages             | Show package details                  |
| winget list \| sort | Sort alphabetically (kinda) | --versions<br>List available versions | --versions<br>List available versions |
### Install \ Uninstall

| _WinGet install {package}_                                          | _WinGet uninstall {package}_                            |
| ------------------------------------------------------------------- | ------------------------------------------------------- |
| **Alias**: _add_                                                    | **Alias**: _remove_ \ _rm_                              |
| winget install --id _Microsoft.PowerToys_ --v _0.15.2_              | winget uninstall --name _powertoys_ --version _0.15.2_  |
| --location \ -l _<­path>_<br>Location to install to (if supported). | --purge<br>Purge the package directory (portable only). |
### Upgrade

| _WinGet upgrade_            | **Alias**: _update_                                                       |
| --------------------------- | ------------------------------------------------------------------------- |
| --include-unknown \ -u      | Include packages that their current version cannot be determined.         |
| --all \ --recurse \ -r      | **Directly begin** updating all installed packages to the latest version. |
| --silent \ -h               | Runs the installer in silent mode. This suppresses all UI.                |
| --pinned \ --include-pinned | Include pinned packages that don't have a **blocking** pin.               |
| --force                     | Run the command and continue with non security related issues.            |
| --uninstall-previous        | Uninstall the previous version prior the upgrade. (Package dependent)     |
```PowerShell
winget upgrade -u           # Display all available updates, include unknown
winget upgrade -u -r -h     # Begin all updates in silent mode, include unknown
```

> ### **💡 Note**  
>The only ways to initiate the upgrade process are either — specifying which packages to upgrade, such as `winget upgrade Obsidian`, or — using  `--all`, `--recurse` or `-r` arguments when upgrading all installed packages, such as `winget upgrade --all`. Otherwise, `winget upgrade` merely lists the available updates and the different arguments alter this list or affect the upgrade process – but they will not initiate it.
### Pin

| _WinGet pin_                                                      |                                    |
| ----------------------------------------------------------------- | ---------------------------------- |
| winget pin add _powershell_                                       | Add a new pin.                     |
| winget pin add --id _Microsoft.PowerShell_ **--blocking**         | Add a blocking pin.                |
| winget pin add --id _Microsoft.PowerShell_ **--version** _0.70.*_ | Add a gating pin.                  |
| winget pin remove _powershell_                                    | Remove a pin.                      |
| winget pin list                                                   | List all current pins.             |
| winget pin list --id _Microsoft.PowerShell_                       | List a pin for a matching ID.      |
| winget pin reset                                                  | Show all pins that would be reset. |
| winget pin reset --force                                          | Reset all existing pins.           |
> ### 📌 **Pin Types:**  
> - ***Regular Pin:***  
> Prevents a package from being upgraded when calling `winget upgrade --all`. Use `--pinned` or `--include-pinned` arguments with `winget upgrade --all` to include pinned packages.
> - ***Blocking Pin:***  
> Prevents a package from being upgraded when calling `winget upgrade --all` or `winget upgrade <package>`. You will need to unblock the package to let WinGet perform an upgrade.
> - ***Gating Pin:***  
> Adding a gating pin will prevent upgrades that upgrade the package version outside of a specific version or the gated wildcard range.

### Export \ Import

| WinGet _export_ -o _packages.json_    |                                                       |
| ------------------------------------- | ----------------------------------------------------- |
| --output \ -o _<path/to/myapps.json>_ | Path to the JSON file to be created.                  |
| --source \ -s _winget_                | Specify a source to export from.                      |
| --include-versions                    | Include versions of the currently installed packages. |

| WinGet _import_ -i _packages.json_         |                                                   |
| ------------------------------------------ | ------------------------------------------------- |
| --import-file \ -i _<path/to/myapps.json>_ | Path to the JSON file to import from.             |
| --ignore-versions                          | Ignore specified versions and install the latest. |
### Download

| _WinGet download {package}_         |                                                                                                |
| ----------------------------------- | ---------------------------------------------------------------------------------------------- |
| --installer-type _msix_             | Select installer type: _portable, exe, msstore,<br>msix, msi, zip, inno, wix, burn, nullsoft_. |
| --architecture \ -a  _x64_          | Select architecture: _x64, x86, arm, arm64_.                                                   |
| --download-directory \ -d _<­path>_ | Select download path.                                                                          |
### WinGet

| WinGet _settings_   |                                 | _WinGet --info_       |                         |
| ------------------- | ------------------------------- | --------------------- | ----------------------- |
| **Alias**: _config_ | Open settings.json              | winget --info         | Display system metadata |
| winget features     | Available experimental features | winget --version \ -v | Display WinGet version  |
### Source

| WinGet _source_                                        |                                                       |
| ------------------------------------------------------ | ----------------------------------------------------- |
| winget source list (**Alias**: _ls_)                   | Display a list of all sources.                        |
| winget source list --name (**Alias**: _n_) _<­source>_ | Display information about a source.                   |
| winget source update (**Alias**: _refresh_)            | Update all sources.                                   |
| winget source update --name _<­source>_                | Update a source by name.                              |
| winget source add --name _<­source> <­url>_            | Add a new source repository.                          |
| winget source remove (**Alias**: _rm_) -n _<­source>_  | Remove a source repository.                           |
| winget source reset --force                            | Reset to original configuration, removes all sources. |
| winget source export _<­source>_                       | Export source details to JSON output.                 |
### Hash \ Manifest

| Miscellaneous                                  |                                                   |
| ---------------------------------------------- | ------------------------------------------------- |
| winget hash _myInstaller.msixbundle_           | Generates installer hash for submitting software. |
| winget hash -f _myInstaller.msixbundle_ --msix | Supports SHA256 certificate hash for MSIX files.  |
| winget validate --manifest _myfile.yml_        | Validates a manifest for submitting software.     |

### Additional Resources
[Windows Package Manager - Overview & Commands](https://learn.microsoft.com/en-us/windows/package-manager/winget/)
[Settings JSON Schema file](https://github.com/microsoft/winget-cli/blob/master/schemas/JSON/settings/settings.schema.0.2.json)