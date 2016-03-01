# 更改通知

## Silder 绑定到 TextBlock，不使用更改通知

首先定义一个简单的类 BindingSlider，同时在 XAML 中作如下定义。

```
    public class BindingSlider
    {
        private int sliderValue;
        public int SliderValue
        {
            get
            {
                return sliderValue;
            }
            set
            {
                sliderValue = value;
            }
        }
    }
```

```
<StackPanel Orientation="Vertical" HorizontalAlignment="Center" VerticalAlignment="Center">
    <Slider Name="slider1" Minimum="0" Maximum="100" Width="200" Value="{Binding SliderValue,Mode=TwoWay}"/>
    <Button x:Name="button" Content="Button" Width="200" Click="button_Click"/>
    <TextBlock Name="textBlock" FontSize="30"/>
</StackPanel>
```

虽然这里只是用到了 OneWay 传递，但还是需要使用 TwoWay。因为在这里 OneWay 是指从 BindingSlider 类的 SliderValue 属性单向传递到 Slider 控件的 Value 属性。但我们需要的则是 Slider 控件的 Value 属性单向传递到 BindingSlider 类的 SliderValue 属性，所以才得使用 TwoWay 方式。

```
        BindingSlider bindingSlider = new BindingSlider();
        public MainPage()
        {
            this.InitializeComponent();
            slider1.DataContext = bindingSlider;
        }
        private void button_Click(object sender, RoutedEventArgs e)
        {
            textBlock.Text = bindingSlider.SliderValue.ToString();
        }
```

首先实例化 BindingSlider 类，再在后台代码中奖 bindingSlider 对象绑定到 slider1 的数据上下文。最后通过 Click 事件来将 bindingSlider 对象的 SliderValue 属性传递给 textBlock 控件的 Text 属性。

这里的效果就是，拖动 Slider 但是 TextBlock 不会有变化，而需要 Button 来不断的更改 TextBlock 的 Text。如果想要 TextBlock 的 Text 能够根据 Slider 实时的更改，这就需要”更改通知“了。

## Silder 绑定到 TextBlock，使用更改通知

既然要使用通知更改的技术，那就可以在 XAML 代码中将 Button 控件删除掉了，包括后台代码中的 Click 事件。

紧接着来修改 BindingSlider 类，首先得使用 INotifyPropertyChanged 接口。这个接口有 PropertyChanged 事件，而这个事件则会告知绑定目标绑定源已经发生修改，这样绑定目标也会实时的进行更改。在新的 set 中，我们将 SliderValue 值传递到 NotifyPropertyChanged 中。

```
    public class BindingSlider :INotifyPropertyChanged
    {
        private int sliderValue;
        public int SliderValue
        {
            get
            {
                return sliderValue;
            }
            set
            {
                sliderValue = value;
                NotifyPropertyChanged("SliderValue");     
            }
        }                                                                           
        public event PropertyChangedEventHandler PropertyChanged;
        public void NotifyPropertyChanged(string propertyName)
        {
            if (PropertyChanged != null)
            {
                PropertyChanged(this,
                    new PropertyChangedEventArgs(propertyName));
            }
        }
    }
```

最后我们还需要将 bindingSlider 对象绑定到 textBlock 的数据上下文。

```
        BindingSlider bindingSlider = new BindingSlider();
        public MainPage()
        {
            this.InitializeComponent();
            slider1.DataContext = bindingSlider;
            textBlock.DataContext = bindingSlider;           
        }
```

这样一来就全部更改完成了，试试就会发现 TextBlock 的 Text 会根据 Slider 的拖动而实时修改了。