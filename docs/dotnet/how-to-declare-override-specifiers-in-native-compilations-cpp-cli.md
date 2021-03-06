---
title: '如何：在 c + +/CLI (声明重写说明符) '
ms.date: 11/04/2016
helpviewer_keywords:
- override specifiers in native compilation, overriding
ms.assetid: d0551836-9ac7-41eb-a6e9-a4b3ef60767d
ms.openlocfilehash: 92bdc41cf9ebe2389f2d22dab211029899283266
ms.sourcegitcommit: 94893973211d0b254c8bcdcf0779997dcc136b0c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2020
ms.locfileid: "91414589"
---
# <a name="how-to-declare-override-specifiers-in-native-compilations-ccli"></a>如何：声明本机编译中的重写说明符 (C++/CLI)

不使用 **/ZW**或[/clr](../build/reference/clr-common-language-runtime-compilation.md)的编译中提供了[sealed](../extensions/sealed-cpp-component-extensions.md)、 [abstract](../extensions/abstract-cpp-component-extensions.md)和[override](../extensions/override-cpp-component-extensions.md) 。

> [!NOTE]
> ISO c + + 11 标准语言具有 [替代](../cpp/override-specifier.md) 标识符和 [最终](../cpp/final-specifier.md) 标识符，在 Visual Studio 中使用 `final` 而不是 **`sealed`** 在要编译为仅限本机的代码中使用。

## <a name="example-sealed-is-valid"></a>示例：密封有效

### <a name="description"></a>说明

下面的示例演示了 **`sealed`** 在本机编译中有效的。

### <a name="code"></a>代码

```cpp
// sealed_native_keyword.cpp
#include <stdio.h>
__interface I1 {
   virtual void f();
   virtual void g();
};

class X : public I1 {
public:
   virtual void g() sealed {}
};

class Y : public X {
public:

   // the following override generates a compiler error
   virtual void g() {}   // C3248 X::g is sealed!
};
```

## <a name="example-override-is-valid"></a>示例：重写有效

### <a name="description"></a>说明

下一个示例显示了 `override` 在本机编译中有效的。

### <a name="code"></a>代码

```cpp
// override_native_keyword.cpp
#include <stdio.h>
__interface I1 {
   virtual void f();
};

class X : public I1 {
public:
   virtual void f() override {}   // OK
   virtual void g() override {}   // C3668 I1::g does not exist
};
```

## <a name="example-abstract-is-valid"></a>示例： abstract 有效

### <a name="description"></a>说明

此示例显示 **`abstract`** 了在本机编译中有效的。

### <a name="code"></a>代码

```cpp
// abstract_native_keyword.cpp
class X abstract {};

int main() {
   X * MyX = new X;   // C3622 cannot instantiate abstract class
}
```

## <a name="see-also"></a>请参阅

[重写说明符](../extensions/override-specifiers-cpp-component-extensions.md)
