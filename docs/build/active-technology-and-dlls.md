---
title: Active 技术和 DLL
ms.date: 11/04/2016
helpviewer_keywords:
- in-process server DLLs
- Automation [C++], DLLs
- DLLs [C++], Active Technology
- Active technology [C++]
- MFC DLLs [C++], Active Technology
ms.assetid: 3ed27f8d-164a-4562-ad61-9f2333404cc7
ms.openlocfilehash: f67fb9548601ac705ceda08d20d3049f0bf1e0a5
ms.sourcegitcommit: da32511dd5baebe27451c0458a95f345144bd439
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2019
ms.locfileid: "65220996"
---
# <a name="active-technology-and-dlls"></a>Active 技术和 DLL

Active 技术使对象服务器得以在 DLL 内完全实现。 此类型的服务器称为进程内服务器。 MFC 不完全支持进程内服务器来实现可视编辑的所有功能，这主要是因为 Active 技术不提供使服务器挂钩到容器主消息循环中的方法。 MFC 需要访问容器应用程序的消息循环才能处理快捷键和空闲时间处理。

如果在编写自动化服务器而且该服务器没有用户界面，则可使该服务器成为进程内服务器并将其完全置于 DLL 中。

## <a name="what-do-you-want-to-know-more-about"></a>你想进一步了解什么？

- [自动化服务器](../mfc/automation-servers.md)

## <a name="see-also"></a>请参阅

[在 Visual Studio 中创建 C/C++ DLL](dlls-in-visual-cpp.md)
