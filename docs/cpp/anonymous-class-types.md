---
title: 匿名类类型
ms.date: 11/04/2016
helpviewer_keywords:
- class types [C++], anonymous
- anonymous class types
ms.assetid: 9ba667b2-8c2a-4c29-82a6-fa120b9233c8
ms.openlocfilehash: 77f0a5517cee5e4baeacbbdcae47bdeea2853a97
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2020
ms.locfileid: "87216630"
---
# <a name="anonymous-class-types"></a>匿名类类型

类可以是匿名的，也就是说，可以在不使用*标识符*的情况下声明它们。 将类名替换为名称时，这会很有用 **`typedef`** ，如下所示：

```cpp
typedef struct
{
    unsigned x;
    unsigned y;
} POINT;
```

> [!NOTE]
> 上面示例中显示的匿名类的用法对于保留与现有 C 代码的兼容性很有用。 在某些 C 代码中，将 **`typedef`** 与匿名结构结合使用非常普遍。

如果您希望对类成员的引用就像它未包含在独立类中的情况一样出现，则匿名类也很有用，如下所示：

```cpp
struct PTValue
{
    POINT ptLoc;
    union
    {
        int  iValue;
        long lValue;
    };
};

PTValue ptv;
```

在前面的代码中， `iValue` 可以使用对象成员选择运算符（**.**）访问，如下所示：

```cpp
int i = ptv.iValue;
```

匿名类受某些限制的约束。 （有关匿名联合的详细信息，请参阅[联合](../cpp/unions.md)。）匿名类：

- 不能具有构造函数或析构函数。

- 不能作为函数的参数传递（除非使用省略号使类型检查无效）。

- 无法作为函数中的返回值返回。

## <a name="anonymous-structs"></a>匿名结构

**Microsoft 专用**

利用 Microsoft C 扩展，您可以在另一个结构中声明结构变量，而无需为其指定名称。 这些嵌套结构称为匿名结构。 C++ 不允许匿名结构。

您可以像访问包含结构中的成员一样访问匿名结构的成员。

```cpp
// anonymous_structures.c
#include <stdio.h>

struct phone
{
    int  areacode;
    long number;
};

struct person
{
    char   name[30];
    char   gender;
    int    age;
    int    weight;
    struct phone;    // Anonymous structure; no name needed
} Jim;

int main()
{
    Jim.number = 1234567;
    printf_s("%d\n", Jim.number);
}
//Output: 1234567
```

**结束 Microsoft 专用**
