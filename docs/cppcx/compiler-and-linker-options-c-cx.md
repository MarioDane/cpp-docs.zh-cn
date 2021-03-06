---
title: 编译器和链接器选项 (C++/CX)
ms.date: 01/22/2017
ms.assetid: ecfadce8-3a3f-40cc-bb01-b4731f8d2fcb
ms.openlocfilehash: cc1964c57d6700995bb283c245e4c63c8e9e313b
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62383355"
---
# <a name="compiler-and-linker-options-ccx"></a>编译器和链接器选项 (C++/CX)

环境变量， C++/CX 编译器选项和 Windows 运行时支持的应用程序生成的链接器选项。

## <a name="library-path"></a>库路径

%LIBPATH% 环境变量指定用于搜索 .winmd 文件的默认路径。

## <a name="compiler-options"></a>编译器选项

|选项|描述|
|------------|-----------------|
|[/ZW](../build/reference/zw-windows-runtime-compilation.md)<br /><br /> /ZW:nostdlib|启用 Windows 运行时语言扩展。<br /><br /> `nostdlib` 参数可阻止编译器使用标准的预定义搜索路径来查找程序集和 .winmd 文件。<br /><br /> **/ZW** 编译器选项隐式指定以下编译器选项：<br /><br />- **/FI** vccorlib.h，这会强制包含 vccorlib.h 头文件，该文件定义编译器所需的许多类型。<br />- [/FU](../build/reference/fu-name-forced-hash-using-file.md) Windows.winmd，这会强制包含 Windows.winmd 元数据文件提供的操作系统，Windows 运行时中定义了许多类型。<br />- **/FU** Platform.winmd，这会强制包含 Platform.winmd 元数据文件，该文件由编译器提供，定义命名空间的 Platform 系列中的大多数类型。|
|[/AI](../build/reference/ai-specify-metadata-directories.md) *dir*|向编译器用于查找程序集和 .winmd 文件的搜索路径添加目录（由 *dir* 参数指定）。|
|**/FU**  *文件*|强制包含指定模块或 .winmd 文件。 即，不必在源代码中指定 `#using`*file* 。 编译器会自动强制包含自己的 Windows 元数据文件 Platform.winmd。|
|/D "WINAPI_FAMILY=2"|创建允许使用与 Windows 运行时兼容的 Win32 sdk 子集的定义。|

## <a name="linker-options"></a>链接器选项

|选项|描述|
|------------|-----------------|
|/APPCONTAINER[:NO]|将可执行文件标记为可在 appcontainer（仅限）中运行。|
|/WINMD[:{NO&#124;ONLY}]|发出 .winmd 文件和关联的二进制文件。 此选项必须传递给链接器，才能发出 .winmd。<br /><br /> **NO**- 不发出 .winmd 文件，但是发出二进制文件。<br /><br /> **ONLY**- 发出 .winmd 文件，但是不发出二进制文件。|
|/WINMDFILE:*filename*|要发出的 .winmd 文件的名称，而不是默认 .winmd 文件名。 如果在命令行上指定了多个文件名，则使用最后一个名称。|
|/WINMDDELAYSIGN[:NO]|对 .winmd 文件进行部分签名并将公钥置于二进制文件中。<br /><br /> **NO**-（默认）不对 .winmd 文件进行签名。<br /><br /> 除非还指定了 /WINMDKEYFILE 或 /WINMDKEYCONTAINER，否则 /WINMDDELAYSIGN 不会产生任何效果。|
|/WINMDKEYCONTAINER:*name*|指定用来对程序集进行签名的密钥容器。 *name* 参数对应于用于对元数据文件进行签名的密钥容器。|
|/WINMDKEYFILE:*filename*|指定用于对程序集进行签名的密钥或密钥对。 *filename* 参数对应于用于对元数据文件进行签名的密钥。|

### <a name="remarks"></a>备注

使用 **/ZW**时，编译器会自动链接到 DLL 版本的 C 运行时 (CRT)。 不允许链接到静态库版本，并且不允许在通用 Windows 平台应用中的 CRT 任何的函数使用将导致编译时错误。

## <a name="see-also"></a>请参阅

[生成应用和库](../cppcx/building-apps-and-libraries-c-cx.md)
