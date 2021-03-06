---
title: time_put 类
ms.date: 11/04/2016
f1_keywords:
- xloctime/std::time_put
- locale/std::time_put::char_type
- locale/std::time_put::iter_type
- locale/std::time_put::do_put
- locale/std::time_put::put
helpviewer_keywords:
- std::time_put [C++]
- std::time_put [C++], char_type
- std::time_put [C++], iter_type
- std::time_put [C++], do_put
- std::time_put [C++], put
ms.assetid: df79493e-3331-48d2-97c3-ac3a745f0791
ms.openlocfilehash: 4f7b609493e16d3d1c0a9ab6274ed6f5bfd7b033
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2020
ms.locfileid: "87212106"
---
# <a name="time_put-class"></a>time_put 类

类模板描述可用作区域设置 facet 的对象，以便控制时间值到类型序列的转换 `CharType` 。

## <a name="syntax"></a>语法

```cpp
template <class CharType,
    class OutputIterator = ostreambuf_iterator<CharType>>
class time_put : public locale::facet;
```

### <a name="parameters"></a>参数

*CharType*\
在程序中用于对字符进行编码的类型。

*OutputIterator*\
供时间放置函数写入其输出结果的迭代器类型。

## <a name="remarks"></a>备注

对于任何区域设置 facet，静态对象 ID 的初始存储值为零。 首次尝试访问其存储值后，将在 **ID** 中存储唯一正值。

### <a name="constructors"></a>构造函数

|构造函数|描述|
|-|-|
|[time_put](#time_put)|`time_put` 类型的对象的构造函数。|

### <a name="typedefs"></a>Typedef

|类型名称|描述|
|-|-|
|[char_type](#char_type)|一种类型，此类型用于描述区域设置使用的字符。|
|[iter_type](#iter_type)|一种类型，此类型描述输出迭代器。|

### <a name="member-functions"></a>成员函数

|成员函数|说明|
|-|-|
|[do_put](#do_put)|一种以 `CharType` 序列的形式输出时间和日期信息的虚拟函数。|
|[准备](#put)|以 `CharType` 的形式输出时间和日期信息。|

## <a name="requirements"></a>要求

**标头：**\<locale>

**命名空间:** std

## <a name="time_putchar_type"></a><a name="char_type"></a>time_put：： char_type

一种类型，此类型用于描述区域设置使用的字符。

```cpp
typedef CharType char_type;
```

### <a name="remarks"></a>备注

类型是模板参数 `CharType` 的同义词。

## <a name="time_putdo_put"></a><a name="do_put"></a>time_put：:d o_put

一种以 `CharType` 序列的形式输出时间和日期信息的虚拟函数。

```cpp
virtual iter_type do_put(
    iter_type next,
    ios_base& _Iosbase,
    const tm* _Pt,
    char _Fmt,
    char _Mod = 0) const;
```

### <a name="parameters"></a>参数

*一个*\
一个输出迭代器，其中字符序列表示要插入的时间和日期。

*_Iosbase*\
未使用。

*_Pt*\
输出的时间和日期信息。

*_Fmt*\
输出格式。 有关有效值的范围，请参阅 [strftime、wcsftime、_strftime_l、_wcsftime_l](../c-runtime-library/reference/strftime-wcsftime-strftime-l-wcsftime-l.md)。

*_Mod*\
格式的修饰符。 有关有效值的范围，请参阅 [strftime、wcsftime、_strftime_l、_wcsftime_l](../c-runtime-library/reference/strftime-wcsftime-strftime-l-wcsftime-l.md)。

### <a name="return-value"></a>返回值

插入最后一个元素后第一个位置的迭代器。

### <a name="remarks"></a>备注

受保护的虚拟成员函数将 `next` 从存储在对象 \* `_Pt` 的类型为的值开始生成连续元素 `tm` 。 该函数返回一个迭代器，指定在生成的输出外下一个要插入元素的位置。

输出由使用的相同规则生成 `strftime` ，其中最后一个参数为 *_Pt*的，用于生成一系列 **`char`** 元素到数组中。 假定每个此类 **`char`** 元素都 `CharType` 按简单的一对一映射映射到类型的等效元素。 如果 *_Mod*等于零，则有效格式为 "% F"，其中 F 替换为 *_Fmt*。 否则，有效格式为 "% MF"，其中 M 替换为 *_Mod*。

### <a name="example"></a>示例

请参阅 [put](#put) 的示例，它调用 `do_put`。

## <a name="time_putiter_type"></a><a name="iter_type"></a>time_put：： iter_type

一种类型，此类型描述输出迭代器。

```cpp
typedef OutputIterator iter_type;
```

### <a name="remarks"></a>备注

类型是模板参数 `OutputIterator` 的同义词。

## <a name="time_putput"></a><a name="put"></a>time_put：:p

以 `CharType` 的形式输出时间和日期信息。

```cpp
iter_type put(iter_type next,
    ios_base& _Iosbase,
    char_type _Fill,
    const tm* _Pt,
    char _Fmt,
    char _Mod = 0) const;

iter_type put(iter_type next,
    ios_base& _Iosbase,
    char_type _Fill,
    const tm* _Pt,
    const CharType* first,
    const CharType* last) const;
```

### <a name="parameters"></a>参数

*一个*\
一个输出迭代器，其中字符序列表示要插入的时间和日期。

*_Iosbase*\
未使用。

*_Fill*\
用于间距的类型的字符 `CharType` 。

*_Pt*\
输出的时间和日期信息。

*_Fmt*\
输出格式。 有关有效值的范围，请参阅 [strftime、wcsftime、_strftime_l、_wcsftime_l](../c-runtime-library/reference/strftime-wcsftime-strftime-l-wcsftime-l.md)。

*_Mod*\
格式的修饰符。 有关有效值的范围，请参阅 [strftime、wcsftime、_strftime_l、_wcsftime_l](../c-runtime-library/reference/strftime-wcsftime-strftime-l-wcsftime-l.md)。

*1*\
输出格式字符串的开头。 有关有效值的范围，请参阅 [strftime、wcsftime、_strftime_l、_wcsftime_l](../c-runtime-library/reference/strftime-wcsftime-strftime-l-wcsftime-l.md)。

*时间*\
输出格式字符串的末尾。 有关有效值的范围，请参阅 [strftime、wcsftime、_strftime_l、_wcsftime_l](../c-runtime-library/reference/strftime-wcsftime-strftime-l-wcsftime-l.md)。

### <a name="return-value"></a>返回值

插入最后一个元素后第一个位置的迭代器。

### <a name="remarks"></a>备注

第一个成员函数返回[do_put](#do_put)（ `next` 、 `_Iosbase` 、 `_Fill` 、 `_Pt` 、 `_Fmt` 、 `_Mod` ）。 第二个成员函数复制到除 \* `next` `first` `last` 百分比（%）以外的间隔 [，）中的任何元素。 对于间隔 [，）中后跟字符*C*的百分比 `first` `last` ，该函数将计算结果 `next`  =  `do_put` （ `next` 、 `_Iosbase` 、 `_Fill` 、 `_Pt` 、 *C*、0），并跳过*C*。然而，如果*C*是 set EOQ # 中的限定符字符，后跟 `C2` 间隔 [，）中的字符 `first` `last` ，则该函数将改为计算 `next`  =  `do_put` （ `next` ， `_Iosbase` ， `_Fill` ， `_Pt` ， `C2` ， *C*），并跳过 `C2` 。

### <a name="example"></a>示例

```cpp
// time_put_put.cpp
// compile with: /EHsc
#include <locale>
#include <iostream>
#include <sstream>
#include <time.h>
using namespace std;
int main( )
{
   locale loc;
   basic_stringstream<char> pszPutI;
   ios_base::iostate st = 0;
   struct tm t;
   memset( &t, 0, sizeof( struct tm ) );

   t.tm_hour = 5;
   t.tm_min = 30;
   t.tm_sec = 40;
   t.tm_year = 00;
   t.tm_mday = 4;
   t.tm_mon = 6;

   pszPutI.imbue( loc );
   char *pattern = "x: %X %x";
   use_facet <time_put <char> >
   (loc).put(basic_ostream<char>::_Iter(pszPutI.rdbuf( )),
          pszPutI, ' ', &t, pattern, pattern+strlen(pattern));

      cout << "num_put( ) = " << pszPutI.rdbuf( )->str( ) << endl;

      char strftimebuf[255];
      strftime(&strftimebuf[0], 255, pattern, &t);
      cout << "strftime( ) = " << &strftimebuf[0] << endl;
}
```

```Output
num_put( ) = x: 05:30:40 07/04/00
strftime( ) = x: 05:30:40 07/04/00
```

## <a name="time_puttime_put"></a><a name="time_put"></a>time_put：： time_put

类型为 `time_put` 的对象的构造函数。

```cpp
explicit time_put(size_t _Refs = 0);
```

### <a name="parameters"></a>参数

*_Refs*\
用于指定对象的内存管理类型的整数值。

### <a name="remarks"></a>备注

*_Refs*参数的可能值及其重要性为：

- 0：对象的生存期由包含该对象的区域设置管理。

- 1：必须手动管理对象的生存期。

- \>1：未定义这些值。

构造函数通过[locale：： facet](../standard-library/locale-class.md#facet_class)（*_Refs*）初始化其基对象。

## <a name="see-also"></a>另请参阅

[\<locale>](../standard-library/locale.md)\
[time_base 类](../standard-library/time-base-class.md)\
[C + + 标准库中的线程安全](../standard-library/thread-safety-in-the-cpp-standard-library.md)
