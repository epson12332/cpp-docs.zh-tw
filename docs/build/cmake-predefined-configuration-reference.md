---
title: 預先定義的 CMake 組態參考
ms.description: Visual Studio provides several predefined build configurations for CMake projects on Linux, Windows, ARM, and IoT.
ms.date: 03/05/2019
helpviewer_keywords:
- CMake redefined configurations
ms.openlocfilehash: d1e77db7ddc38fa41771a512a5b863d403bfdc28
ms.sourcegitcommit: 8105b7003b89b73b4359644ff4281e1595352dda
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/14/2019
ms.locfileid: "57824944"
---
# <a name="cmake-predefined-build-configurations"></a>CMake 預先定義的組建組態

在 CMake 專案中，組建組態會儲存在的 CMakeSettings.json 檔案。 當您選擇**管理組態**從在主要工具列組建組態下拉式清單，對話方塊隨即出現，顯示的預設 Visual Studio 中的 CMake 組態： 
- x86 偵錯 
- x86 版本
- x64 偵錯
- x64 版本
- Linux 偵錯
- Linux-Release
- IoT 偵錯
- IoT 版本
- MinGW 偵錯
- MinGW 版本 

當您選擇的設定時，會將它新增至專案的根資料夾中的 CMakeSettings.json 檔案。 您接著可以使用它來建置您的專案。 


## <a name="linux-predefined-build-configurations"></a>預先定義的 Linux 組建組態：

```json
{
      "name": "Linux-Debug",
      "generator": "Unix Makefiles",
      "remoteMachineName": "user@host",
      "configurationType": "Debug",
      "remoteCMakeListsRoot": "/var/tmp/src/${workspaceHash}/${name}",
      "cmakeExecutable": "/usr/local/bin/cmake",
      "buildRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\build\\${name}",
      "installRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\install\\${name}",
      "remoteBuildRoot": "/var/tmp/build/${workspaceHash}/build/${name}",
      "remoteInstallRoot": "/var/tmp/build/${workspaceHash}/install/${name}",
      "remoteCopySources": true,
      "remoteCopySourcesOutputVerbosity": "Normal",
      "remoteCopySourcesConcurrentCopies": "10",
      "remoteCopySourcesMethod": "rsync",
      "remoteCopySourcesExclusionList": [
        ".vs",
        ".git"
      ],
      "rsyncCommandArgs": "-t --delete --delete-excluded",
      "remoteCopyBuildOutput": false,
      "cmakeCommandArgs": "",
      "buildCommandArgs": "",
      "ctestCommandArgs": "",
      "inheritEnvironments": [
        "linux_x64"
      ]
    }

{
      "name": "Linux-Release",
      "generator": "Unix Makefiles",
      "remoteMachineName": "${defaultRemoteMachineName}",
      "configurationType": "RelWithDebInfo",
      "remoteCMakeListsRoot": "/var/tmp/src/${workspaceHash}/${name}",
      "cmakeExecutable": "/usr/local/bin/cmake",
      "buildRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\build\\${name}",
      "installRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\install\\${name}",
      "remoteBuildRoot": "/var/tmp/build/${workspaceHash}/build/${name}",
      "remoteInstallRoot": "/var/tmp/build/${workspaceHash}/install/${name}",
      "remoteCopySources": true,
      "remoteCopySourcesOutputVerbosity": "Normal",
      "remoteCopySourcesConcurrentCopies": "10",
      "remoteCopySourcesMethod": "rsync",
      "remoteCopySourcesExclusionList": [
        ".vs",
        ".git"
      ],
      "rsyncCommandArgs": "-t --delete --delete-excluded",
      "remoteCopyBuildOutput": false,
      "cmakeCommandArgs": "",
      "buildCommandArgs": "",
      "ctestCommandArgs": "",
      "inheritEnvironments": [
        "linux_x64"
      ]
    },
    ```


You can use these optional settings for more control:

```json
{
      "remotePreBuildCommand": "",
      "remotePreGenerateCommand": "",
      "remotePostBuildCommand": "",
}
```

這些選項可讓您之前和之後建置和 CMake 產生前，在遠端系統上執行命令。 值可以是任何有效遠端系統的命令。 輸出會經由管道輸出，回到 Visual Studio。

## <a name="iot-predefined-build-configurations"></a>IoT 預先定義的組建組態

```json
{
      "name": "IoT-Debug",
      "generator": "Ninja",
      "configurationType": "Debug",
      "inheritEnvironments": [
        "gcc-arm"
      ],
      "buildRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\build\\${name}",
      "installRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\install\\${name}",
      "cmakeCommandArgs": "",
      "buildCommandArgs": "-v",
      "ctestCommandArgs": "",
      "intelliSenseMode": "linux-gcc-arm",
      "variables": [
        {
          "name": "CMAKE_C_COMPILER",
          "value": "arm-none-eabi-gcc.exe"
        },
        {
          "name": "CMAKE_CXX_COMPILER",
          "value": "arm-none-eabi-g++.exe"
        },
        {
          "name": "CMAKE_C_FLAGS",
          "value": "-nostartfiles"
        },
        {
          "name": "CMAKE_CXX_FLAGS",
          "value": "-nostartfiles -fno-rtti -fno-exceptions"
        },
        {
          "name": "CMAKE_CXX_STANDARD",
          "value": "14"
        },
        {
          "name": "CMAKE_SYSTEM_NAME",
          "value": "Generic"
        },
        {
          "name": "CMAKE_SYSTEM_PROCESSOR",
          "value": "arm"
        }
      ]
    },
    {
      "name": "IoT-Release",
      "generator": "Ninja",
      "configurationType": "Release",
      "inheritEnvironments": [
        "gcc-arm"
      ],
      "buildRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\build\\${name}",
      "installRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\install\\${name}",
      "cmakeCommandArgs": "",
      "buildCommandArgs": "-v",
      "ctestCommandArgs": "",
      "intelliSenseMode": "linux-gcc-arm",
      "variables": [
        {
          "name": "CMAKE_C_COMPILER",
          "value": "arm-none-eabi-gcc.exe"
        },
        {
          "name": "CMAKE_CXX_COMPILER",
          "value": "arm-none-eabi-g++.exe"
        },
        {
          "name": "CMAKE_C_FLAGS",
          "value": "-nostartfiles"
        },
        {
          "name": "CMAKE_CXX_FLAGS",
          "value": "-nostartfiles -fno-rtti -fno-exceptions"
        },
        {
          "name": "CMAKE_CXX_STANDARD",
          "value": "14"
        },
        {
          "name": "CMAKE_SYSTEM_NAME",
          "value": "Generic"
        },
        {
          "name": "CMAKE_SYSTEM_PROCESSOR",
          "value": "arm"
        }
      ]
    }
```

## <a name="mingw-predefined-build-configurations"></a>MinGW 預先定義的組建組態

```json
{
      "environments": [
        {
          "MINGW64_ROOT": "C:\\msys64\\mingw64",
          "BIN_ROOT": "${env.MINGW64_ROOT}\\bin",
          "FLAVOR": "x86_64-w64-mingw32",
          "TOOLSET_VERSION": "7.3.0",
          "PATH": "${env.MINGW64_ROOT}\\bin;${env.MINGW64_ROOT}\\..\\usr\\local\\bin;${env.MINGW64_ROOT}\\..\\usr\\bin;${env.MINGW64_ROOT}\\..\\bin;${env.PATH}",
          "INCLUDE": "${env.INCLUDE};${env.MINGW64_ROOT}\\include\\c++\\${env.TOOLSET_VERSION};${env.MINGW64_ROOT}\\include\\c++\\${env.TOOLSET_VERSION}\\tr1;${env.MINGW64_ROOT}\\include\\c++\\${env.TOOLSET_VERSION}\\${env.FLAVOR}",
          "environment": "mingw_64"
        }
      ],
      "name": "Mingw64-Debug",
      "generator": "Ninja",
      "configurationType": "Debug",
      "inheritEnvironments": [
        "mingw_64"
      ],
      "buildRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\build\\${name}",
      "installRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\install\\${name}",
      "cmakeCommandArgs": "",
      "buildCommandArgs": "-v",
      "ctestCommandArgs": "",
      "intelliSenseMode": "linux-gcc-x64",
      "variables": [
        {
          "name": "CMAKE_C_COMPILER",
          "value": "${env.BIN_ROOT}\\gcc.exe"
        },
        {
          "name": "CMAKE_CXX_COMPILER",
          "value": "${env.BIN_ROOT}\\g++.exe"
        }
      ]
    }

{
      "environments": [
        {
          "MINGW64_ROOT": "C:\\msys64\\mingw64",
          "BIN_ROOT": "${env.MINGW64_ROOT}\\bin",
          "FLAVOR": "x86_64-w64-mingw32",
          "TOOLSET_VERSION": "7.3.0",
          "PATH": "${env.MINGW64_ROOT}\\bin;${env.MINGW64_ROOT}\\..\\usr\\local\\bin;${env.MINGW64_ROOT}\\..\\usr\\bin;${env.MINGW64_ROOT}\\..\\bin;${env.PATH}",
          "INCLUDE": "${env.INCLUDE};${env.MINGW64_ROOT}\\include\\c++\\${env.TOOLSET_VERSION};${env.MINGW64_ROOT}\\include\\c++\\${env.TOOLSET_VERSION}\\tr1;${env.MINGW64_ROOT}\\include\\c++\\${env.TOOLSET_VERSION}\\${env.FLAVOR}",
          "environment": "mingw_64"
        }
      ],
      "name": "Mingw64-Release",
      "generator": "Ninja",
      "configurationType": "RelWithDebInfo",
      "inheritEnvironments": [
        "mingw_64"
      ],
      "buildRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\build\\${name}",
      "installRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\install\\${name}",
      "cmakeCommandArgs": "",
      "buildCommandArgs": "-v",
      "ctestCommandArgs": "",
      "intelliSenseMode": "linux-gcc-x64",
      "variables": [
        {
          "name": "CMAKE_C_COMPILER",
          "value": "${env.BIN_ROOT}\\gcc.exe"
        },
        {
          "name": "CMAKE_CXX_COMPILER",
          "value": "${env.BIN_ROOT}\\g++.exe"
        }
      ]
    }
```

## <a name="x86-64-predefined-build-configurations"></a>x86 64 預先定義的組建組態

```json
    {
      "name": "x86-Debug",
      "generator": "Ninja",
      "configurationType": "Debug",
      "inheritEnvironments": [
        "msvc_x86"
      ],
      "buildRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\build\\${name}",
      "installRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\install\\${name}",
      "cmakeCommandArgs": "",
      "buildCommandArgs": "-v",
      "ctestCommandArgs": ""
    },
    {
      "name": "x86-Release",
      "generator": "Ninja",
      "configurationType": "RelWithDebInfo",
      "inheritEnvironments": [
        "msvc_x86"
      ],
      "buildRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\build\\${name}",
      "installRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\install\\${name}",
      "cmakeCommandArgs": "",
      "buildCommandArgs": "-v",
      "ctestCommandArgs": ""
    },
    {
      "name": "x64-Debug",
      "generator": "Ninja",
      "configurationType": "Debug",
      "inheritEnvironments": [
        "msvc_x64_x64"
      ],
      "buildRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\build\\${name}",
      "installRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\install\\${name}",
      "cmakeCommandArgs": "",
      "buildCommandArgs": "-v",
      "ctestCommandArgs": ""
    },
    {
      "name": "x64-Release",
      "generator": "Ninja",
      "configurationType": "RelWithDebInfo",
      "inheritEnvironments": [
        "msvc_x64_x64"
      ],
      "buildRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\build\\${name}",
      "installRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\install\\${name}",
      "cmakeCommandArgs": "",
      "buildCommandArgs": "-v",
      "ctestCommandArgs": ""
    },
    {
      "name": "x86-Release2",
      "generator": "Ninja",
      "configurationType": "RelWithDebInfo",
      "inheritEnvironments": [
        "msvc_x86"
      ],
      "buildRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\build\\${name}",
      "installRoot": "${env.USERPROFILE}\\CMakeBuilds\\${workspaceHash}\\install\\${name}",
      "cmakeCommandArgs": "",
      "buildCommandArgs": "-v",
      "ctestCommandArgs": ""
    }
  ]
}
```

## <a name="see-also"></a>另請參閱

[Visual Studio 中的 CMake 專案](cmake-projects-in-visual-studio.md)<br/>
[設定 Linux CMake 專案](../linux/cmake-linux-project.md)<br/>
[連線到遠端 Linux 電腦](../linux/connect-to-your-remote-linux-computer.md)<br/>
[設定 CMake 偵錯工作階段](configure-cmake-debugging-sessions.md)<br/>
[部署、執行及偵錯 Linux 專案](../linux/deploy-run-and-debug-your-linux-project.md)<br/>
[預先定義的 CMake 組態參考](cmake-predefined-configuration-reference.md)<br/>