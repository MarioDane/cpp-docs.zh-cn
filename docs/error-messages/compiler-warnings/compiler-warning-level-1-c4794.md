---
title: 编译器警告（等级 1）C4794
ms.date: 11/04/2016
f1_keywords:
- C4794
helpviewer_keywords:
- C4794
ms.assetid: badc9c36-fa1a-4fec-929b-7bfda7a7b79f
ms.openlocfilehash: 7f7ea7555937069caf5f83c9bf00f0fa980ef020
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/24/2020
ms.locfileid: "80175111"
---
# <a name="compiler-warning-level-1-c4794"></a>编译器警告（等级 1）C4794

线程本地存储区变量“variable”的段由“section name”改为“.tls$”

你使用了 [#pragma data_seg](../../preprocessor/data-seg.md) 向未以 .tls$ 开始的节中放置 tls 变量。

.Tls$*x* 节将出现在定义了 [__declspec (thread)](../../cpp/thread.md) 变量的对象文件中。 EXE 或 DLL 中的 .tls 节将从这些节中产生。

## <a name="example"></a>示例

下面的示例生成 C4794：

```cpp
// C4794.cpp
// compile with: /W1 /c
#pragma data_seg(".someseg")
__declspec(thread) int i;   // C4794

// OK
#pragma data_seg(".tls$9")
__declspec(thread) int j;
```
