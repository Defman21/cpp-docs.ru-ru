---
description: 'Дополнительные сведения: операции Windows (C++/CLI)'
title: Операции Windows (C++/CLI)
ms.date: 11/04/2016
helpviewer_keywords:
- Windows [C++], Windows-specific tasks
- .NET Framework [C++], Windows operations
- Visual C++, Windows operations
- Windows operations [C++]
- .NET Framework, shutdown
- shutdown
- termination
- applications [C++], shutdown
- Visual C++, user interactive state
- user interactive state
- Visual C++, reading from Windows Registry
- registry, reading
- performance counters
- performance counters, reading Windows performance counters
- performance monitoring, Windows performance counters
- performance, counters
- counters, reading Windows performance counters
- performance
- performance monitoring
- text, retrieving from Clipboard
- Clipboard, retrieving text
- current user names
- user names, retrieving
- UserName string
- .NET Framework, version
- Version property, retrieving .NET Framework version
- computer name, retrieving
- machine name, retrieving
- computer name
- Windows [C++], version
- Windows [C++], retrieving version using Visual C++
- time, elapsed since startup
- counters, elapsed time
- startup, time elapsed since
- tick counts
- startup
- text, storing in Clipboard
- Clipboard, storing text
- registry, writing to
- Visual C++, writing to Windows Registry
ms.assetid: b9a75cb4-0589-4d5b-92cb-5e8be42b4ac0
ms.openlocfilehash: 95fff25cb5c921272972e343dd3a85d53f909c52
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97298725"
---
# <a name="windows-operations-ccli"></a>Операции Windows (C++/CLI)

Демонстрирует различные задачи, относящиеся к Windows, с использованием Windows SDK.

В следующих разделах демонстрируются различные операции Windows, выполняемые с Windows SDK с помощью Visual C++.

## <a name="determine-if-shutdown-has-started"></a><a name="determine_shutdown"></a> Определить, запущено ли завершение работы

В следующем примере кода показано, как определить, завершается ли в данный момент приложение или .NET Framework. Это полезно для доступа к статическим элементам в .NET Framework поскольку во время завершения работы эти конструкции завершаются системой и не могут быть надежно использованы. Сначала проверив <xref:System.Environment.HasShutdownStarted%2A> свойство, можно избежать потенциальных сбоев, не обращаясь к этим элементам.

### <a name="example"></a>Пример

```cpp
// check_shutdown.cpp
// compile with: /clr
using namespace System;
int main()
{
   if (Environment::HasShutdownStarted)
      Console::WriteLine("Shutting down.");
   else
      Console::WriteLine("Not shutting down.");
   return 0;
}
```

## <a name="determine-the-user-interactive-state"></a><a name="determine_user"></a> Определение интерактивного состояния пользователя

В следующем примере кода показано, как определить, выполняется ли код в интерактивном контексте пользователя. Если <xref:System.Environment.UserInteractive%2A> имеет значение false, то код выполняется как процесс службы или в веб-приложении. в этом случае не следует пытаться взаимодействовать с пользователем.

### <a name="example"></a>Пример

```cpp
// user_interactive.cpp
// compile with: /clr
using namespace System;

int main()
{
   if ( Environment::UserInteractive )
      Console::WriteLine("User interactive");
   else
      Console::WriteLine("Noninteractive");
   return 0;
}
```

## <a name="read-data-from-the-windows-registry"></a><a name="read_registry"></a> Чтение данных из реестра Windows

В следующем примере кода используется <xref:Microsoft.Win32.Registry.CurrentUser> ключ для чтения данных из реестра Windows. Во-первых, подразделы перечисляются с помощью <xref:Microsoft.Win32.RegistryKey.GetSubKeyNames%2A> метода, а затем подраздел удостоверений открывается с помощью <xref:Microsoft.Win32.RegistryKey.OpenSubKey%2A> метода. Как и корневые ключи, каждый подраздел представлен <xref:Microsoft.Win32.RegistryKey> классом. Наконец, <xref:Microsoft.Win32.RegistryKey> для перечисления пар "ключ-значение" используется новый объект.

### <a name="example"></a>Пример

```cpp
// registry_read.cpp
// compile with: /clr
using namespace System;
using namespace Microsoft::Win32;

int main( )
{
   array<String^>^ key = Registry::CurrentUser->GetSubKeyNames( );

   Console::WriteLine("Subkeys within CurrentUser root key:");
   for (int i=0; i<key->Length; i++)
   {
      Console::WriteLine("   {0}", key[i]);
   }

   Console::WriteLine("Opening subkey 'Identities'...");
   RegistryKey^ rk = nullptr;
   rk = Registry::CurrentUser->OpenSubKey("Identities");
   if (rk==nullptr)
   {
      Console::WriteLine("Registry key not found - aborting");
      return -1;
   }

   Console::WriteLine("Key/value pairs within 'Identities' key:");
   array<String^>^ name = rk->GetValueNames( );
   for (int i=0; i<name->Length; i++)
   {
      String^ value = rk->GetValue(name[i])->ToString();
      Console::WriteLine("   {0} = {1}", name[i], value);
   }

   return 0;
}
```

### <a name="remarks"></a>Комментарии

<xref:Microsoft.Win32.Registry>Класс является просто контейнером для статических экземпляров <xref:Microsoft.Win32.RegistryKey> . Каждый экземпляр представляет корневой узел реестра. Экземпляры:,,, <xref:Microsoft.Win32.Registry.ClassesRoot> <xref:Microsoft.Win32.Registry.CurrentConfig> <xref:Microsoft.Win32.Registry.CurrentUser> <xref:Microsoft.Win32.Registry.LocalMachine> и <xref:Microsoft.Win32.Registry.Users> .

Помимо статического, объекты в <xref:Microsoft.Win32.Registry> классе доступны только для чтения. Кроме того, экземпляры <xref:Microsoft.Win32.RegistryKey> класса, созданные для доступа к содержимому объектов реестра, также доступны только для чтения. Пример переопределения этого поведения см. в разделе [практические руководства. запись данных в реестр Windows (C++/CLI)](#write_data).

В классе есть два дополнительных объекта <xref:Microsoft.Win32.Registry> : <xref:Microsoft.Win32.Registry.DynData> и <xref:Microsoft.Win32.Registry.PerformanceData> . Оба являются экземплярами <xref:Microsoft.Win32.RegistryKey> класса. <xref:Microsoft.Win32.Registry.DynData>Объект содержит динамические сведения реестра, которые поддерживаются только в windows 98 и Windows Me. <xref:Microsoft.Win32.Registry.PerformanceData>Объект можно использовать для доступа к сведениям счетчика производительности приложений, использующих систему наблюдения за производительностью Windows. <xref:Microsoft.Win32.Registry.PerformanceData>Узел представляет сведения, которые фактически не хранятся в реестре и поэтому не могут быть просмотрены с помощью Regedit.exe.

## <a name="read-windows-performance-counters"></a><a name="read_performance"></a> Чтение счетчиков производительности Windows

Некоторые приложения и подсистемы Windows предоставляют данные о производительности с помощью системы производительности Windows. Доступ к этим счетчикам можно получить с помощью <xref:System.Diagnostics.PerformanceCounterCategory> <xref:System.Diagnostics.PerformanceCounter> классов и, которые находятся в <xref:System.Diagnostics?displayProperty=fullName> пространстве имен.

В следующем примере кода эти классы используются для извлечения и отображения счетчика, обновляемого Windows, чтобы указать процент времени, в течение которого процессор занят.

> [!NOTE]
> В этом примере требуются права администратора для работы в Windows Vista.

### <a name="example"></a>Пример

```cpp
// processor_timer.cpp
// compile with: /clr
#using <system.dll>

using namespace System;
using namespace System::Threading;
using namespace System::Diagnostics;
using namespace System::Timers;

ref struct TimerObject
{
public:
   static String^ m_instanceName;
   static PerformanceCounter^ m_theCounter;

public:
   static void OnTimer(Object^ source, ElapsedEventArgs^ e)
   {
      try
      {
         Console::WriteLine("CPU time used: {0,6} ",
          m_theCounter->NextValue( ).ToString("f"));
      }
      catch(Exception^ e)
      {
         if (dynamic_cast<InvalidOperationException^>(e))
         {
            Console::WriteLine("Instance '{0}' does not exist",
                  m_instanceName);
            return;
         }
         else
         {
            Console::WriteLine("Unknown exception... ('q' to quit)");
            return;
         }
      }
   }
};

int main()
{
   String^ objectName = "Processor";
   String^ counterName = "% Processor Time";
   String^ instanceName = "_Total";

   try
   {
      if ( !PerformanceCounterCategory::Exists(objectName) )
      {
         Console::WriteLine("Object {0} does not exist", objectName);
         return -1;
      }
   }
   catch (UnauthorizedAccessException ^ex)
   {
      Console::WriteLine("You are not authorized to access this information.");
      Console::Write("If you are using Windows Vista, run the application with ");
      Console::WriteLine("administrative privileges.");
      Console::WriteLine(ex->Message);
      return -1;
   }

   if ( !PerformanceCounterCategory::CounterExists(
          counterName, objectName) )
   {
      Console::WriteLine("Counter {0} does not exist", counterName);
      return -1;
   }

   TimerObject::m_instanceName = instanceName;
   TimerObject::m_theCounter = gcnew PerformanceCounter(
          objectName, counterName, instanceName);

   System::Timers::Timer^ aTimer = gcnew System::Timers::Timer();
   aTimer->Elapsed += gcnew ElapsedEventHandler(&TimerObject::OnTimer);
   aTimer->Interval = 1000;
   aTimer->Enabled = true;
   aTimer->AutoReset = true;

   Console::WriteLine("reporting CPU usage for the next 10 seconds");
   Thread::Sleep(10000);
   return 0;
}
```

## <a name="retrieve-text-from-the-clipboard"></a><a name="retrieve_text"></a> Извлечение текста из буфера обмена

В следующем примере кода функция- <xref:System.Windows.Forms.Clipboard.GetDataObject%2A> член используется для возвращения указателя на <xref:System.Windows.Forms.IDataObject> интерфейс. Затем этот интерфейс может запрашивать формат данных и использоваться для получения фактических данных.

### <a name="example"></a>Пример

```cpp
// read_clipboard.cpp
// compile with: /clr
#using <system.dll>
#using <system.Drawing.dll>
#using <system.windows.forms.dll>

using namespace System;
using namespace System::Windows::Forms;

[STAThread] int main( )
{
   IDataObject^ data = Clipboard::GetDataObject( );

   if (data)
   {
      if (data->GetDataPresent(DataFormats::Text))
      {
         String^ text = static_cast<String^>
           (data->GetData(DataFormats::Text));
         Console::WriteLine(text);
      }
      else
         Console::WriteLine("Nontext data is in the Clipboard.");
   }
   else
   {
      Console::WriteLine("No data was found in the Clipboard.");
   }

   return 0;
}
```

## <a name="retrieve-the-current-username"></a><a name="retrieve_current"></a> Получение текущего имени пользователя

В следующем примере кода показано получение имени текущего пользователя (имя пользователя, вошедшего в Windows). Имя хранится в <xref:System.Environment.UserName%2A> строке, которая определена в <xref:System.Environment> пространстве имен.

### <a name="example"></a>Пример

```cpp
// username.cpp
// compile with: /clr
using namespace System;

int main()
{
   Console::WriteLine("\nCurrent user: {0}", Environment::UserName);
   return 0;
}
```

## <a name="retrieve-the-net-framework-version"></a><a name="retrieve_dotnet"></a> Получение версии .NET Framework

В следующем примере кода показано, как определить версию установленного .NET Framework со <xref:System.Environment.Version%2A> свойством, которое является указателем на <xref:System.Version> объект, содержащий сведения о версии.

### <a name="example"></a>Пример

```cpp
// dotnet_ver.cpp
// compile with: /clr
using namespace System;
int main()
{
   Version^ version = Environment::Version;
   if (version)
   {
      int build = version->Build;
      int major = version->Major;
      int minor = version->Minor;
      int revision = Environment::Version->Revision;
      Console::Write(".NET Framework version: ");
      Console::WriteLine("{0}.{1}.{2}.{3}",
            build, major, minor, revision);
   }
   return 0;
}
```

## <a name="retrieve-the-local-machine-name"></a><a name="retrieve_local"></a> Получение имени локального компьютера

В следующем примере кода показано получение имени локального компьютера (имя компьютера в том виде, в котором оно отображается в сети). Это можно сделать, получив <xref:System.Environment.MachineName%2A> строку, которая определена в <xref:System.Environment> пространстве имен.

### <a name="example"></a>Пример

```cpp
// machine_name.cpp
// compile with: /clr
using namespace System;

int main()
{
   Console::WriteLine("\nMachineName: {0}", Environment::MachineName);
   return 0;
}
```

## <a name="retrieve-the-windows-version"></a><a name="retrieve_version"></a> Получение версии Windows

В следующем примере кода показано, как получить сведения о платформе и версии текущей операционной системы. Эта информация хранится в <xref:System.Environment.OSVersion%2A?displayProperty=fullName> свойстве и состоит из перечисления, описывающего версию Windows в широком смысле, и <xref:System.Environment.Version%2A> объект, содержащий точную сборку операционной системы.

### <a name="example"></a>Пример

```cpp
// os_ver.cpp
// compile with: /clr
using namespace System;

int main()
{
   OperatingSystem^ osv = Environment::OSVersion;
   PlatformID id = osv->Platform;
   Console::Write("Operating system: ");

   if (id == PlatformID::Win32NT)
      Console::WriteLine("Win32NT");
   else if (id == PlatformID::Win32S)
      Console::WriteLine("Win32S");
   else if (id == PlatformID::Win32Windows)
      Console::WriteLine("Win32Windows");
   else
      Console::WriteLine("WinCE");

   Version^ version = osv->Version;
   if (version)
   {
      int build = version->Build;
      int major = version->Major;
      int minor = version->Minor;
      int revision = Environment::Version->Revision;
      Console::Write("OS Version: ");
      Console::WriteLine("{0}.{1}.{2}.{3}",
                   build, major, minor, revision);
   }

   return 0;
}
```

## <a name="retrieve-time-elapsed-since-startup"></a><a name="retrieve_time"></a> Получить время, прошедшее с момента запуска

В следующем примере кода показано, как определить число тактов или число миллисекунд, прошедших с момента запуска Windows. Это значение хранится в элементе <xref:System.Environment.TickCount%2A?displayProperty=fullName> и, поскольку это 32-разрядное значение, сбрасывается в ноль примерно каждые 24,9 дней.

### <a name="example"></a>Пример

```cpp
// startup_time.cpp
// compile with: /clr
using namespace System;

int main( )
{
   Int32 tc = Environment::TickCount;
   Int32 seconds = tc / 1000;
   Int32 minutes = seconds / 60;
   float hours = static_cast<float>(minutes) / 60;
   float days = hours / 24;

   Console::WriteLine("Milliseconds since startup: {0}", tc);
   Console::WriteLine("Seconds since startup: {0}", seconds);
   Console::WriteLine("Minutes since startup: {0}", minutes);
   Console::WriteLine("Hours since startup: {0}", hours);
   Console::WriteLine("Days since startup: {0}", days);

   return 0;
}
```

## <a name="store-text-in-the-clipboard"></a><a name="store_text"></a> Хранение текста в буфере обмена

В следующем примере кода <xref:System.Windows.Forms.Clipboard> для хранения строки используется объект, определенный в <xref:System.Windows.Forms> пространстве имен. Этот объект предоставляет две функции элементов: <xref:System.Windows.Forms.Clipboard.SetDataObject%2A> и <xref:System.Windows.Forms.Clipboard.GetDataObject%2A> . Данные хранятся в буфере обмена путем отправки любого объекта, производного от <xref:System.Object> , в <xref:System.Windows.Forms.Clipboard.SetDataObject%2A> .

### <a name="example"></a>Пример

```cpp
// store_clipboard.cpp
// compile with: /clr
#using <System.dll>
#using <System.Drawing.dll>
#using <System.Windows.Forms.dll>

using namespace System;
using namespace System::Windows::Forms;

[STAThread] int main()
{
   String^ str = "This text is copied into the Clipboard.";

   // Use 'true' as the second argument if
   // the data is to remain in the clipboard
   // after the program terminates.
   Clipboard::SetDataObject(str, true);

   Console::WriteLine("Added text to the Clipboard.");

   return 0;
}
```

## <a name="write-data-to-the-windows-registry"></a><a name="write_data"></a> Запись данных в реестр Windows

В следующем примере кода используется <xref:Microsoft.Win32.Registry.CurrentUser> ключ для создания доступного для записи экземпляра <xref:Microsoft.Win32.RegistryKey> класса, соответствующего **программному** ключу. <xref:Microsoft.Win32.RegistryKey.CreateSubKey%2A>Затем метод используется для создания нового ключа и добавления в пары "ключ-значение".

### <a name="example"></a>Пример

```cpp
// registry_write.cpp
// compile with: /clr
using namespace System;
using namespace Microsoft::Win32;

int main()
{
   // The second OpenSubKey argument indicates that
   // the subkey should be writable.
   RegistryKey^ rk;
   rk  = Registry::CurrentUser->OpenSubKey("Software", true);
   if (!rk)
   {
      Console::WriteLine("Failed to open CurrentUser/Software key");
      return -1;
   }

   RegistryKey^ nk = rk->CreateSubKey("NewRegKey");
   if (!nk)
   {
      Console::WriteLine("Failed to create 'NewRegKey'");
      return -1;
   }

   String^ newValue = "NewValue";
   try
   {
      nk->SetValue("NewKey", newValue);
      nk->SetValue("NewKey2", 44);
   }
   catch (Exception^)
   {
      Console::WriteLine("Failed to set new values in 'NewRegKey'");
      return -1;
   }

   Console::WriteLine("New key created.");
   Console::Write("Use REGEDIT.EXE to verify ");
   Console::WriteLine("'CURRENTUSER/Software/NewRegKey'\n");
   return 0;
}
```

### <a name="remarks"></a>Комментарии

.NET Framework можно использовать для доступа к реестру с помощью <xref:Microsoft.Win32.Registry> классов и <xref:Microsoft.Win32.RegistryKey> , которые определены в <xref:Microsoft.Win32> пространстве имен. Класс **реестра** — это контейнер для статических экземпляров <xref:Microsoft.Win32.RegistryKey> класса. Каждый экземпляр представляет корневой узел реестра. Экземпляры:,,, <xref:Microsoft.Win32.Registry.ClassesRoot> <xref:Microsoft.Win32.Registry.CurrentConfig> <xref:Microsoft.Win32.Registry.CurrentUser> <xref:Microsoft.Win32.Registry.LocalMachine> и <xref:Microsoft.Win32.Registry.Users> .

## <a name="related-sections"></a>Связанные разделы

<xref:System.Environment>

## <a name="see-also"></a>См. также раздел

[Программирование .NET с использованием C++/CLI (Visual C++)](../dotnet/dotnet-programming-with-cpp-cli-visual-cpp.md)
