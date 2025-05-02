# <img src="Windows.svg" alt="Windows 11" width="26"/> WinGet Cheat Sheet

### Query Options

| _--query \ -q_ |                                       | _--query \ -q_    |                              |
| -------------- | ------------------------------------- | ----------------- | ---------------------------- |
| --id           | winget update --id _Mozilla.Firefox_  | --source \ -s     | winget list -source winget   |
| --name         | winget find --name "_Visual Studio_"  | --tag             | winget search --tag _vscode_ |
| --version \ -v | winget remove _powertoys_ -v _0.15.2_ | --help \ -?       | winget <­command> --help     |
| --exact \ -e   | Use the exact string in the query     | --count \ -n _10_ | Limit to _10_ results        |
### List \ Search \ Show

| _WinGet list_       |                             | _WinGet search {package}_ | _WinGet show {package}_ |
| ------------------- | --------------------------- | ------------------------- | ----------------------- |
| **Alias**: _ls_     | List installed packages     | **Alias**: _find_         | **Alias**: _view_       |
| --count \ -n _10_   | Limit to _10_ results       | Search available packages | Show package details    |
| winget list \| sort | Sort alphabetically (kinda) | --versions                | List available versions |
### Install \ Uninstall

| _WinGet install {package}_                             | _WinGet uninstall {package}_                           |
| ------------------------------------------------------ | ------------------------------------------------------ |
| **Alias**: _add_                                       | **Alias**: _remove_ \ _rm_                             |
| winget install --id _Microsoft.PowerToys_ --v _0.15.2_ | winget uninstall --name _powertoys_ --version _0.15.2_ |
### Upgrade

| _WinGet upgrade_            | **Alias**: _update_                                                       |
| --------------------------- | ------------------------------------------------------------------------- |
| --include-unknown \ -u      | Include packages that their current version cannot be determined.         |
| --all \ --recurse \ -r      | **Directly begin** updating all installed packages to the latest version. |
| --silent \ -h               | Runs the installer in silent mode. This suppresses all UI.                |
| --pinned \ --include-pinned | Include pinned packages that don't have a **blocking** pin.               |
| --force                     | Run the command and continue with non security related issues.            |
| --uninstall-previous        | Uninstall the previous version prior the upgrade. (Package dependent)     |
#### **💡 Note**
The only ways to initiate the upgrade process are either — specifying which packages to upgrade, such as `winget upgrade Obsidian`, or — using  `--all`, `--recurse` or `-r` arguments when upgrading all installed packages, such as `winget upgrade --all`. Otherwise, `winget upgrade` merely lists the available updates and the different arguments alter this list or affect the upgrade process – but they will not initiate it.
### Pin

| _WinGet pin_                                                      |                                    |
| ----------------------------------------------------------------- | ---------------------------------- |
| winget pin add _powertoys_                                        | Adds a new pin                     |
| winget pin add --id _Microsoft.PowerShell_ **--blocking**         | Adds a blocking pin                |
| winget pin add --id _Microsoft.PowerShell_ **--version** _0.70.*_ | Adds a gating pin                  |
| winget pin remove _powertoys_                                     | Removes a pin for an application   |
| winget pin list                                                   | Lists all current pins             |
| winget pin list --id _Microsoft.PowerToys_                        | List pin with matching ID          |
| winget pin reset                                                  | Shows all pins that would be reset |
| winget pin reset --force                                          | Resets all existing pins           |
#### 📌 **Pin Options:**
- ***Regular Pin:***  
Prevents a package from being upgraded when calling `winget upgrade --all`. Use `--pinned` or `--include-pinned` arguments with `winget upgrade --all` to include pinned packages.
- ***Blocking Pin:***  
Prevents a package from being upgraded when calling `winget upgrade --all` or `winget upgrade <package>`. You will need to unblock the package to let WinGet perform an upgrade.
- ***Gating Pin:***  
Adding a gating pin will prevent upgrades that upgrade the package version outside of a specific version or the gated wildcard range.

### Export & Import

| WinGet _export_ -o _apps.json_ |                                         | WinGet _import_ -i _apps.json_   |                                       |
| ------------------------------ | --------------------------------------- | -------------------------------- | ------------------------------------- |
| --output \ -o _<path.json>_    | Path to JSON                            | --import-file \ -i _<path.json>_ | Path to JSON                          |
| --include-versions             | Specify currently<br>installed versions | --ignore-versions                | Ignore versions<br>and install latest |
### Download

| _WinGet download {package}_                         |                                             |
| --------------------------------------------------- | ------------------------------------------- |
| winget download _PowerToys_ --installer-type _msix_ | Select installer type                       |
| --architecture \ -a  _x64_                          | Select architecture: _x64, x86, arm, arm64_ |
| --download-directory \ -d _<­path>_                 | Select download path                        |
### Source

| WinGet _source_                                       |                                                      |
| ----------------------------------------------------- | ---------------------------------------------------- |
| winget source list (**Alias**: _ls_)                  | Display all sources or one via -n _<­source>_        |
| winget source add --name _<­source> <­url>_           | Add a new source repository                          |
| winget source update (**Alias**: _refresh_)           | Update all sources or one via -n _<­source>_         |
| winget source remove (**Alias**: _rm_) -n _<­source>_ | Remove a source repository                           |
| winget source reset --force                           | Reset to original configuration, removes all sources |
| winget source export _<­source>_                      | Export source details to JSON output                 |
### WinGet

| WinGet _settings_   |                                 | _WinGet --info_       |                         |
| ------------------- | ------------------------------- | --------------------- | ----------------------- |
| **Alias**: _config_ | Open settings.json              | winget --info         | Display system metadata |
| winget features     | Available experimental features | winget --version \ -v | Display WinGet version  |
### Hash \ Manifest

| Miscellaneous                                  |                                                  |
| ---------------------------------------------- | ------------------------------------------------ |
| winget hash _myInstaller.msixbundle_           | Generates installer hash for submitting software |
| winget hash -f _myInstaller.msixbundle_ --msix | Supports SHA256 certificate hash for MSIX files  |
| winget validate --manifest _myfile.yml_        | Validates a manifest for submitting software     |

[Windows Package Manager - Overview & Commands](https://learn.microsoft.com/en-us/windows/package-manager/winget/)