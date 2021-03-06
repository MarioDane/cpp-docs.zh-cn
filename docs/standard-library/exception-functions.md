---
title: '&lt;exception&gt; 函数'
ms.date: 11/04/2016
f1_keywords:
- exception/std::current_exception
- exception/std::get_terminate
- exception/std::get_unexpected
- exception/std::make_exception_ptr
- exception/std::rethrow_exception
- exception/std::set_terminate
- exception/std::set_unexpected
- exception/std::terminate
- exception/std::uncaught_exception
- exception/std::unexpected
ms.assetid: c09ac569-5e35-4fe8-872d-ca5810274dd7
helpviewer_keywords:
- std::current_exception [C++]
- std::get_terminate [C++]
- std::get_unexpected [C++]
- std::make_exception_ptr [C++]
- std::rethrow_exception [C++]
- std::set_terminate [C++]
- std::set_unexpected [C++]
- std::terminate [C++]
- std::uncaught_exception [C++]
- std::unexpected [C++]
ms.openlocfilehash: 849f3c8406c43b0efc2d34837e00fee6ff64e52a
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2020
ms.locfileid: "87193778"
---
# <a name="ltexceptiongt-functions"></a>&lt;exception&gt; 函数

## <a name="current_exception"></a><a name="current_exception"></a>current_exception

获取指向当前异常的智能指针。

```cpp
exception_ptr current_exception();
```

### <a name="return-value"></a>返回值

指向当前异常的 [exception_ptr](../standard-library/exception-typedefs.md#exception_ptr) 对象。

### <a name="remarks"></a>备注

调用 catch 块中的 `current_exception` 函数。 如果异常处于飞行状态，而且 catch 块可捕获该异常，则 `current_exception` 函数将返回引用该异常的 `exception_ptr` 对象。 否则，该函数将返回 null `exception_ptr` 对象。

`current_exception`函数捕获处于飞行中的异常，而不考虑该 **`catch`** 语句是否指定[异常声明](../cpp/try-throw-and-catch-statements-cpp.md)语句。

如果未再次引发异常，则将在块的末尾调用当前异常的析构函数 **`catch`** 。 但是，即使调用析构函数中的 `current_exception` 函数，该函数仍返回引用当前异常的 `exception_ptr` 对象。

对 `current_exception` 函数的相继调用将返回引用当前异常的不同副本的 `exception_ptr` 对象。 因此，由于对象引用不同的副本，即使副本具有相同的二进制值，其比较结果也是不相等。

## <a name="make_exception_ptr"></a><a name="make_exception_ptr"></a>make_exception_ptr

创建保留异常副本的 [exception_ptr](../standard-library/exception-typedefs.md#exception_ptr) 对象。

```cpp
template <class E>
    exception_ptr make_exception_ptr(E Except);
```

### <a name="parameters"></a>参数

*只有*\
具有要复制的异常的类。 通常，指定[异常类](../standard-library/exception-class.md)对象作为参数传递给 `make_exception_ptr` 函数，但任意类对象都可以是参数。

### <a name="return-value"></a>返回值

指向的当前异常副本的[exception_ptr](../standard-library/exception-typedefs.md#exception_ptr)对象*除外*。

### <a name="remarks"></a>备注

调用 `make_exception_ptr` 函数等效于引发 C++ 异常、在 catch 块中捕获它并调用 [current_exception](../standard-library/exception-functions.md#current_exception) 函数以返回引用异常的 `exception_ptr` 对象。 Microsoft 实现的 `make_exception_ptr` 函数比调用并捕获异常更高效。

应用程序通常不需要 `make_exception_ptr` 函数，因此，我们不建议使用此函数。

## <a name="rethrow_exception"></a><a name="rethrow_exception"></a>rethrow_exception

引发作为参数传递的异常。

```cpp
void rethrow_exception(exception_ptr P);
```

### <a name="parameters"></a>参数

*H-p*\
要再次引发的已捕获异常。 如果*P*为空[exception_ptr](../standard-library/exception-typedefs.md#exception_ptr)，则函数将引发[std：： bad_exception](../standard-library/bad-exception-class.md)。

### <a name="remarks"></a>备注

在 `exception_ptr` 对象中存储捕获的异常后，主线程便可以处理该对象。 在主线程中，调用 `rethrow_exception` 函数，将 `exception_ptr` 对象作为其参数。 `rethrow_exception` 函数从 `exception_ptr` 对象中提取异常，然后在主线程的上下文中引发异常。

## <a name="get_terminate"></a><a name="get_terminate"></a>get_terminate

获取当前的 `terminate_handler` 函数。

```cpp
terminate_handler get_terminate();
```

## <a name="set_terminate"></a><a name="set_terminate"></a>set_terminate

建立程序终止时要调用的新 `terminate_handler`。

```cpp
terminate_handler set_terminate(terminate_handler fnew) throw();
```

### <a name="parameters"></a>参数

*fnew*\
终止时要调用的函数。

### <a name="return-value"></a>返回值

上一个在终止时用于调用的函数的地址。

### <a name="remarks"></a>备注

函数会建立新的[terminate_handler](../standard-library/exception-typedefs.md#terminate_handler)作为函数 * *fnew*。 因此， *fnew*不能为 null 指针。 函数将返回上一个终止处理程序的地址。

### <a name="example"></a>示例

```cpp
// exception_set_terminate.cpp
// compile with: /EHsc
#include <exception>
#include <iostream>

using namespace std;

void termfunction()
{
    cout << "My terminate function called." << endl;
    abort();
}

int main()
{
    terminate_handler oldHandler = set_terminate(termfunction);

    // Throwing an unhandled exception would also terminate the program
    // or we could explicitly call terminate();

    //throw bad_alloc();
    terminate();
}
```

## <a name="get_unexpected"></a><a name="get_unexpected"></a>get_unexpected

获取当前的 `unexpected_handler` 函数。

```cpp
unexpected_handler get_unexpected();
```

## <a name="rethrow_if_nested"></a><a name="rethrow_if_nested"></a>rethrow_if_nested

```cpp
template <class E>
    void rethrow_if_nested(const E& e);
```

### <a name="remarks"></a>备注

如果不是多态类类型，或者如果不可 `nested_exception` 访问或不明确，则不起作用。 否则，执行动态强制转换。

## <a name="set_unexpected"></a><a name="set_unexpected"></a>set_unexpected

建立遇到意外异常时要调用的新 `unexpected_handler`。

```cpp
unexpected_handler set_unexpected(unexpected_handler fnew) throw();
```

### <a name="parameters"></a>参数

*fnew*\
遇到意外异常时要调用的函数。

### <a name="return-value"></a>返回值

上一个 `unexpected_handler` 的地址。

### <a name="remarks"></a>备注

*fnew*不能为 null 指针。

C++ 标准要求在函数引发其引发列表中未包含的异常时调用 `unexpected`。 当前实现不支持此操作。 以下示例直接调用 `unexpected`，后者随后调用 `unexpected_handler`。

### <a name="example"></a>示例

```cpp
// exception_set_unexpected.cpp
// compile with: /EHsc
#include <exception>
#include <iostream>

using namespace std;

void uefunction()
{
    cout << "My unhandled exception function called." << endl;
    terminate(); // this is what unexpected() calls by default
}

int main()
{
    unexpected_handler oldHandler = set_unexpected(uefunction);

    unexpected(); // library function to force calling the
                  // current unexpected handler
}
```

## <a name="terminate"></a><a name="terminate"></a>终止

调用终止处理程序。

```cpp
void terminate();
```

### <a name="remarks"></a>备注

函数调用终止处理程序，它是类型的函数 **`void`** 。 如果 `terminate` 由程序直接调用，则终止处理程序是通过调用[set_terminate](../standard-library/exception-functions.md#set_terminate)最近设置的处理程序。 如果在 `terminate` 计算 throw 表达式的过程中有多个其他原因调用了，则终止处理程序是在计算 throw 表达式后立即生效的处理程序。

终止处理程序可能不会返回至其调用方。 在程序启动时，终止处理程序是调用的函数 `abort` 。

### <a name="example"></a>示例

有关 `terminate` 的使用示例，请参阅 [set_unexpected](../standard-library/exception-functions.md#set_unexpected)。

## <a name="throw_with_nested"></a><a name="throw_with_nested"></a>throw_with_nested

```cpp
template <class T> [[noreturn]]
    void throw_with_nested(T&& t);
```

### <a name="remarks"></a>备注

引发带有嵌套异常的异常。

## <a name="uncaught_exception"></a><a name="uncaught_exception"></a>uncaught_exception

**`true`** 仅当当前正在处理引发的异常时返回。

```cpp
bool uncaught_exception();
```

### <a name="return-value"></a>返回值

在 **`true`** 完成 throw 表达式的求值后，以及在匹配处理程序中完成异常声明的初始化之前返回，或在引发表达式的结果中调用[意外](../standard-library/exception-functions.md#unexpected)之前返回。 特别是， `uncaught_exception` **`true`** 当从异常展开过程中调用的析构函数调用时，将返回。 在设备上，仅 Windows CE 5.00 及更高版本（包括 Windows Mobile 2005 平台）支持 `uncaught_exception`。

### <a name="example"></a>示例

```cpp
// exception_uncaught_exception.cpp
// compile with: /EHsc
#include <exception>
#include <iostream>
#include <string>

class Test
{
public:
   Test( std::string msg ) : m_msg( msg )
   {
      std::cout << "In Test::Test(\"" << m_msg << "\")" << std::endl;
   }
   ~Test( )
   {
      std::cout << "In Test::~Test(\"" << m_msg << "\")" << std::endl
         << "        std::uncaught_exception( ) = "
         << std::uncaught_exception( )
         << std::endl;
   }
private:
    std::string m_msg;
};

// uncaught_exception will be true in the destructor
// for the object created inside the try block because
// the destructor is being called as part of the unwind.

int main( void )
   {
      Test t1( "outside try block" );
      try
      {
         Test t2( "inside try block" );
         throw 1;
      }
      catch (...) {
   }
}
```

```Output
In Test::Test("outside try block")
In Test::Test("inside try block")
In Test::~Test("inside try block")
        std::uncaught_exception( ) = 1
In Test::~Test("outside try block")
        std::uncaught_exception( ) = 0
```

## <a name="unexpected"></a><a name="unexpected"></a>之外

调用意外处理程序。

```cpp
void unexpected();
```

### <a name="remarks"></a>备注

C++ 标准要求在函数引发其引发列表中未包含的异常时调用 `unexpected`。 当前实现不支持此操作。 此示例直接调用会调用意外处理程序的 `unexpected`。

函数调用类型的异常处理程序 **`void`** 。 如果直接通过程序调用了 `unexpected`，则此意外处理程序是最近通过对 [set_unexpected](../standard-library/exception-functions.md#set_unexpected) 的调用设置的那一个。

意外处理程序可能不会返回其调用方。 其可能通过以下方式终止执行：

- 引发异常规范中所列出的类型的对象，或如果直接通过程序调用了意外处理程序，则引发任意类型的对象。

- 引发 [bad_exception](../standard-library/bad-exception-class.md) 类型的对象。

- 调用[terminate](../standard-library/exception-functions.md#terminate) `abort` 或 `exit` 。

程序启动时，意外处理程序是调用 [terminate](../standard-library/exception-functions.md#terminate) 的函数。

### <a name="example"></a>示例

有关 `unexpected` 的使用示例，请参阅 [set_unexpected](../standard-library/exception-functions.md#set_unexpected)。
