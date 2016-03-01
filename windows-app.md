# Windows App 简介

## C#

C# 是微软主推的编程语言，也是 Windows App 最合适的开发语言，因此本教程统一用 C# 来讲解。

开发 Windows App，可以用 Windows XAML（C#、C++ 和 VB）、WinJS（HTML＋JavaScript）、DirectX（C++）等组合。而 Silverlight（C# 和 VB）是 WP 所独有的，Silverlight 已经基本被淘汰，建议大家用 C#+XAML 来进行开发，在游戏开发和图像处理方面，C++ 则更有优势。

## XAML

Extensible Application Markup Language（简称 XAML，发音为 Zamel）是 WPF 的一部分，其语法类似于HTML，它们都是“标记语言”。我是先学的 XAML 后学的 HTML，一开始还很喜欢这种语言——它没有一大堆的“；”。XAML 本质上属于一种 .NET 编程语言，属于公共语言运行时（Common Language Runtime，简称 CLR）。

看到很多的教程等上都在一开始便讲解了 xmlns 等命名空间，我觉得这样不太合适，毕竟现在根本用不到，因此也记不住，等到需要的时候自然会印象深刻。

## 通用应用

其实我觉得“通用应用“这个名字显然更加合适，更加侧重”通用“的特点。其能够在所有的 Windows 平台上运行，不仅仅是 PC、平板、手机，甚至还有 Xbox。能够在多个平台共享大部分的代码，使其能够一次开发，在多平台运行。

虽然跨平台大家都在做，但通用应用这个概念我还是挺看好的。此前一直有 Windows 10 要兼容安卓应用的传闻，在微软 2015 Build 大会上，微软宣布的则是通过将安卓应用极为方便快速地移植到 Windows 平台，虽然这样一来由于应用设计风格的巨大差异会特色渐消。此外 Windows 10 的免费升级计划是否能通过桌面版带动移动版的发展，让我们拭目以待吧。