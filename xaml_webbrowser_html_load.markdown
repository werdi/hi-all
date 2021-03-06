# XAML
## WPF: загрузка html в WebBrowser из ресурсов
 Есть следующий xaml, в котором определен WebBrowser:
 ```xml
 <Window x:Class="WpfApplication6.Window1"
 xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
 xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
 Title="Window1" Height="300" Width="300">
 <WebBrowser x:Name="_Wb" Margin="20" />
 </Window>
 ```

Требуется загрузить в WebBrowser содержимое файла, например, Content.htm, который добавлен в проект как ресурс, т.е. в свойствах файла указан Build Action: Resource).
 Для этого в конструктор класса Window1 надо добавить следующий код:
 ```C# 
 Uri uri = new Uri(@"pack://application:,,,/Content.htm", UriKind.Absolute);
 Stream source = Application.GetResourceStream(uri).Stream;
 _Wb.NavigateToStream(source);
 ```

 P.S.
 Ресурсный файл Content.htm можно сделать "подфайлом" для Window.xaml, т.е. Content.htm станет соседом для 
 Window.xaml.cs; для этого надо в файле проекта (файл с расширением .csproj) заменить 
 ```xml 
 <Resource Include="Window1.htm" />
 ```
 на 
 ```xml 
 <Resource Include="Window1.htm">
 <DependentUpon>Window1.xaml</DependentUpon>
</Resource>
```
В Visual Studio в появившемся диалоге "File Modification Detected" нажать Reload. 
