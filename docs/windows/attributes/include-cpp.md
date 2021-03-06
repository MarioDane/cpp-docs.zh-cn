---
title: '包括 (c + + COM 特性) '
ms.date: 10/02/2018
f1_keywords:
- vc-attr.include
helpviewer_keywords:
- include attribute
ms.assetid: d23f8b91-fe5b-48fa-9371-8bd73af7b8e3
ms.openlocfilehash: 6b75df74ee69ee4f89eb7bf18fb6bcd77d8a6284
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88842190"
---
# <a name="include-c"></a>include (C++)

指定要包含在生成的 .idl 文件中的一个或多个标头文件。

## <a name="syntax"></a>语法

```cpp
[ include(header_file) ];
```

### <a name="parameters"></a>参数

*header_file*<br/>
要包含在生成的 .idl 文件中的文件的名称。

## <a name="remarks"></a>注解

**Include** c + + 特性导致 `#include` 语句放置 `import "docobj.idl"` 在生成的 .idl 文件中的语句下方。

**Include** c + + 特性具有与[include](/windows/win32/Midl/include) MIDL 特性相同的功能。

## <a name="example"></a>示例

下面的代码演示如何使用 **include**的示例。 在此示例中，文件包含 .h，只包含一个 `#include` 语句。

```cpp
// cpp_attr_ref_include.cpp
// compile with: /LD
[module(name="MyLib")];
[include(cpp_attr_ref_include.h)];
```

## <a name="requirements"></a>要求

| 特性上下文 | 值 |
|-|-|
|**适用于**|任何位置|
|**且**|否|
|**必需属性**|无|
|**无效的特性**|无|

有关详细信息，请参见 [特性上下文](cpp-attributes-com-net.md#contexts)。

## <a name="see-also"></a>另请参阅

[IDL 特性](idl-attributes.md)<br/>
[独立属性](stand-alone-attributes.md)<br/>
[import](import.md)<br/>
[importidl](importidl.md)<br/>
[includelib](includelib-cpp.md)<br/>
[importlib](importlib.md)
