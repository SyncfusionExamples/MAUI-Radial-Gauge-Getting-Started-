# Getting Started with .NET MAUI Radial Gauge

## Creating an application using the .NET MAUI Radial Gauge

The [.NET MAUI Radial Gauge](https://www.syncfusion.com/maui-controls/maui-radial-gauge?utm_source=github&utm_medium=listing&utm_campaign=maui-radial-gauge-github-samples) is a multi-purpose data visualization control that displays numerical values on a circular scale with customizable axes, ranges, pointers, and annotations. This guide will help you integrate the Radial Gauge control into your .NET MAUI application.

### Step 1: Create a new .NET MAUI application in Visual Studio

1. Go to **File > New > Project** and choose the **.NET MAUI App** template.
2. Name the project and choose a location. Click **Next**.
3. Select the .NET framework version and click **Create**.

### Step 2: Install the Syncfusion .NET MAUI Gauges NuGet package

1. In **Solution Explorer**, right-click the project and choose **Manage NuGet Packages**.
2. Search for Syncfusion.Maui.Gauges and install the latest version.
3. Ensure the necessary dependencies are installed correctly, and the project is restored.

### Step 3: Register the Syncfusion handler

Syncfusion.Maui.Core NuGet is a dependent package for all Syncfusion controls of .NET MAUI. In the MauiProgram.cs file, register the handler for Syncfusion core.

**[C#]**
```csharp
using Microsoft.Maui;
using Microsoft.Maui.Hosting;
using Syncfusion.Maui.Core.Hosting;

namespace RadialGaugeGettingStarted
{
    public static class MauiProgram
    {
        public static MauiApp CreateMauiApp()
        {
            var builder = MauiApp.CreateBuilder();
            builder
                .UseMauiApp<App>()
                .ConfigureSyncfusionCore()
                .ConfigureFonts(fonts =>
                {
                    fonts.AddFont("OpenSans-Regular.ttf", "OpenSansRegular");
                });

            return builder.Build();
        }
    }
}
```

### Step 4: Add the Radial Gauge namespace

Import the Gauge namespace to your XAML or C# code.

**[XAML]**
```xaml
xmlns:gauge="clr-namespace:Syncfusion.Maui.Gauges;assembly=Syncfusion.Maui.Gauges"
```

**[C#]**
```csharp
using Syncfusion.Maui.Gauges;
```

### Step 5: Initialize the Radial Gauge

Initialize the [SfRadialGauge](https://www.syncfusion.com/maui-controls/maui-radial-gauge) and configure axes, ranges, and pointers to display your data.

**[XAML]**
```xaml
<ContentPage   
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:gauge="clr-namespace:Syncfusion.Maui.Gauges;assembly=Syncfusion.Maui.Gauges"
    x:Class="RadialGaugeGettingStarted.MainPage">

    <Grid>
        <gauge:SfRadialGauge>
            <gauge:SfRadialGauge.Axes>
                <gauge:RadialAxis Interval="10"
								  Maximum="150" >
                    <gauge:RadialAxis.Ranges>
                        <gauge:RadialRange StartValue="0"
										   EndValue="50"
										   Fill="Red" />
                        <gauge:RadialRange StartValue="50"
										   EndValue="100"
										   Fill="Orange" />
                        <gauge:RadialRange StartValue="100"
										   EndValue="150"
										   Fill="Green" />
                    </gauge:RadialAxis.Ranges>
                    <gauge:RadialAxis.Pointers>
                        <gauge:NeedlePointer Value="90" />
                    </gauge:RadialAxis.Pointers>
                    <gauge:RadialAxis.Annotations>
                        <gauge:GaugeAnnotation x:Name="annotation"
											   DirectionUnit="Angle"
											   DirectionValue="90"
											   PositionFactor="0.5">
                            <gauge:GaugeAnnotation.Content>
                                <Label Text="90"
									   FontSize="25"
									   FontAttributes="Bold" 
                                       TextColor="Black"/>
                            </gauge:GaugeAnnotation.Content>
                        </gauge:GaugeAnnotation>
                    </gauge:RadialAxis.Annotations>
                </gauge:RadialAxis>
            </gauge:SfRadialGauge.Axes>
        </gauge:SfRadialGauge>
    </Grid>
</ContentPage>
```

**[C#]**
```csharp
using Syncfusion.Maui.Gauges;
. . .

public partial class MainPage : ContentPage
{
    public MainPage()
    {
        this.InitializeComponent();
        
        SfRadialGauge radialGauge = new SfRadialGauge();
        
		var axis = new RadialAxis
		{
			Interval = 10,
			Maximum = 150
		};

		// Ranges
		axis.Ranges.Add(new RadialRange
		{
			StartValue = 0,
			EndValue = 50,
			Fill = Colors.Red
		});

		axis.Ranges.Add(new RadialRange
		{
			StartValue = 50,
			EndValue = 100,
			Fill = Colors.Orange
		});

		axis.Ranges.Add(new RadialRange
		{
			StartValue = 100,
			EndValue = 150,
			Fill = Colors.Green
		});

		// Needle Pointer
		axis.Pointers.Add(new NeedlePointer
		{
			Value = 90
		});

		// Annotation
		var annotation = new GaugeAnnotation
		{
			DirectionUnit = AnnotationDirection.Angle,
			DirectionValue = 90,
			PositionFactor = 0.5,
			Content = new Label
			{
				Text = "90",
				FontSize = 25,
				FontAttributes = FontAttributes.Bold,
				TextColor = Colors.Black
			}
		};

		axis.Annotations.Add(annotation);

		// Add axis to gauge
		radialGauge.Axes.Add(axis);

        this.Content = radialGauge;
    }
}
```

![Getting started](MAUI-RadialGauge.png)