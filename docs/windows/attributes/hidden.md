---
title: '隐藏 (c + + COM 特性) '
ms.date: 10/02/2018
f1_keywords:
- vc-attr.hidden
helpviewer_keywords:
- hidden attribute
ms.assetid: 199c96dd-fc07-46c7-af93-92020aebebe7
ms.openlocfilehash: ffa1ce01cfd570de7b699e415f10b27acf525047
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88830951"
---
# <a name="hidden"></a>隐藏

指示该项存在，但不应在面向用户的浏览器中显示。

## <a name="syntax"></a>语法

```cpp
[hidden]
```

## <a name="remarks"></a>备注

**隐藏**的 c + + 特性与[隐藏](/windows/win32/Midl/hidden)的 MIDL 特性具有相同的功能。

## <a name="example"></a>示例

有关如何使用**hidden**的示例，请参阅可[绑定](bindable.md)的示例。

## <a name="requirements"></a>要求

| 特性上下文 | 值 |
|-|-|
|**适用于**|**interface**、 **`class`** ， **`struct`** 、method、property|
|**且**|否|
|**必需属性**|**coclass**当应用于 **`class`** 或) 时，组件类 (**`struct`**|
|**无效的特性**|无|

有关详细信息，请参见 [特性上下文](cpp-attributes-com-net.md#contexts)。

## <a name="see-also"></a>另请参阅

[IDL 特性](idl-attributes.md)<br/>
[接口特性](interface-attributes.md)<br/>
[类特性](class-attributes.md)<br/>
[方法特性](method-attributes.md)
