# 编辑文本及键盘输入

相信大家都会使用 TextBox，但如果要让文本在 TextBox 中换行该怎么做呢？将 TextWrapping 属性设置为 Wrap，将 AcceptsReturn 属性设置为 True 就好。

PasswordBox 很明显就是一个密码框了，和其他的控件相比其有 2 个特殊之处，一个是其可以用 MaxLength 来控制最大的长度，一个是用 PasswordChanged 来捕捉密码的改名。显然比如 QQ 密码的 MaxLength 就是 16 位了，而 PasswordChanged 可以用来监测比如用户设置的密码和用户名是否相同。

大家在用电脑或者手机输入时偶尔键盘是出来的 26 字母拼音或是 26 字母英文亦或是 10 个数字对吧，那这个是怎么实现的呢？同样也是很简单的噢！直接在 TextBox 上用 InputScope 属性就好啦，比如有 Default、TelephoneNumber、EmailSmtpAddress、Url、Search、Chat 等可以设置。

除了在 XAML 中设置 InputScope 属性外，也可以在后台 C# 文件中设置。

```
InputScope inputScope = new InputScope();
InputScopeName inputScopeName= new InputScopeName();
inputScopeName.NameValue = InputScopeNameValue.TelephoneNumber;
inputScope.Names.Add(scopeName);
phoneNumberTtBox.InputScope = scope;
```

在这段代码中，phoneNumberTtBox 是 TextBox 的名字哟，或者也可以简写这段代码的：

```
phoneNumberTtBox.InputScope = new InputScope() 
{
    Names = {new InputScopeName(InputScopeNameValue.TelephoneNumber)}
};
```
除此之外，我们还可以给 `RichEditBox` 控件设置 `IsSpellCheckEnabled` 属性让这个文本控件启用拼写检查。另外值得注意的是 TextBox 控件的拼写检查只在 Windows Phone 上启用，在 Windows 上市禁用的。而文本预测属性在 `TextBox` 和 `RichEditBox` 以及在 Windows 和 Windows Phone 上都是可用的哦，也就是 `IsTextPredictionEnabled`。