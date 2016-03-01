# 时间控件的更多介绍

在前面我们走马观花地介绍了一大堆控件，其中自然也包括这 DatePicker 和 TimePicker，那么稍微高级些的用法呢？

如果你想做一个关于健身、闹钟等的 App，那么不可避免的会用到时间这些控件了。

```
<DatePicker x:Name="datePicker" Header="NoMasp Date" Foreground="Beige"/>          
<Button x:Name="btnOK" Click="btnOK_Click" Content="确定" Foreground="Cyan" Margin= "292,378,0,352" >
     <Button.Flyout>
          <Flyout>
              <TextBlock x:Name="tblock1" Foreground="Fuchsia"/>
          </Flyout>
     </Button.Flyout>
</Button>
```

那么我们可能需要所选定的时间是未来时间，也就是比应用运行时的时间要大。获取当前选中的时间给程序的其他部分使用也是很简单的，我这里的 year 等都在之前定义过了哦，在函数内定义可是不明智的哟。

```
private void btnOK_Click(object sender, RoutedEventArgs e)
{
	if(datePicker.Date>DateTimeOffset.Now)
        tblock1.Text = string.Format("你所选中的时间是：{0}。", datePicker.Date.ToString("D"));
    else
        tblock1.Text = "噢！你想要穿越吗？";    
	year = datePicker.Date.Year;
	month = datePicker.Date.Month;
	day = datePicker.Date.Day;   
}        
```

有意思的事情又来了，如果你是想要做一个时间囊，默认的时间就是 10 年之后，那么 DatePicker 的初始事件如果正好就是 10 年后不是非常好吗。那么我们要做的呢，首先就是给 DatePicker 的 Loaded 写一条事件啦。（虽然我觉得 App 是保存不了 10 年的）

```
private void datePicker_Loaded(object sender, RoutedEventArgs e)
{
    datePicker.Date = DateTimeOffset.Now.AddYears(10);
}
```

如果不想兴师动众去用 DatePicker 的 Loaded，那么也可以直接在后台代码中这样写。

```
protected override void OnNavigatedTo(NavigationEventArgs e)
{
    datePicker.Date = DateTimeOffset.Now.AddYears(10);
}
```
我还做了一个小测试呢，在 Loaded 事件中让时间增加 11 年，在 OnNavigatedTo 事件中让时间增加 10 年，结果——结果是增加了 11 年啦，看来还是自家的 Loaded 更厉害。

接下来就是 TimePicker 啦，回到健身的话题，假设哈，6 点到 18 点才适合运动，那么我们的 Microsoft Band 就做了以下这么个要求（开玩笑啦）。

```
    private void btnOK_Click(object sender, RoutedEventArgs e)
        {
            TimeSpan startTime = new TimeSpan(6, 0, 0);
            TimeSpan endTime = new TimeSpan(18, 0, 0);
            if(timePicker.Time>=startTime&&timePicker.Time<=endTime)
            {
                tblock1.Text = string.Format("这段时间运动都是很好的哦——{0}。", timePicker.Time.ToString());
            }
            else
            {
                tblock1.Text = "此时间吧不适合运动的吧？";
            }       
        }        
```
也许你还想控制手环上时间选择器的初始时间，那么代码来了。

```
protected override void OnNavigatedTo(NavigationEventArgs e)
{                                              
     timePicker.Time = new TimeSpan(23, 0, 0);
}
```

作为强迫症患者呢，每次我设定闹钟的时候都要设置在一个比较好的时间，比如被 5 整除啦、质数啦。这里可以用 MinuteIncrement 属性来控制分钟的增量哟，比如增量为 5 呀。从小学起就飞得把电子手表的时间给设置成 24 小时制的，这个也是可以实现的，ClockIdentifier 设置成 24HourClock 就搞定啦。