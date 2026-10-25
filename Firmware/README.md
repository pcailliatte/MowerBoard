
# OpenMower

## Structure

| Path                         | Purpose                                                                                                                             |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| _build                       | The [CMake build tree](https://cmake.org/cmake/help/latest/manual/cmake.1.html#introduction-to-cmake-buildsystems), can be deleted. |
| cmake                        | Generated [CMake](https://cmake.org/) files. May be deleted if user.cmake has not been added                                        |
| .vscode                      | See [VSCode](https://code.visualstudio.com/docs/getstarted/settings)                                                                |
| .vscode\settings.json        | Workspace specific settings                                                                                                         |
| .vscode\OpenMower.mplab.json | The MPLAB project file, should not be deleted                                                                                       |
| out                          | Final build artifacts                                                                                                               |

## Licence

Le code de ce dossier (hors `config.mcc/`) est sous **GPL-3.0-or-later**, avec une permission additionnelle autorisant la liaison avec le code généré par Microchip MPLAB Code Configurator (MCC). Voir [LICENSE](LICENSE).

Les fichiers de `config.mcc/` sont générés par MCC et restent sous la licence Microchip indiquée dans chaque fichier.
