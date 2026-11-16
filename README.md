
# ==========================================
# NOVA - GOJO INFINITY DESKTOP LAUNCHER
# Windows 11 | PowerShell 5.1 | 4K Ready
# ==========================================

Add-Type -AssemblyName PresentationFramework
Add-Type -AssemblyName PresentationCore
Add-Type -AssemblyName WindowsBase

[xml]$xaml = @'
<Window xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="NOVA - GOJO INFINITY"
        Width="1350" Height="850"
        MinWidth="950" MinHeight="650"
        WindowStartupLocation="CenterScreen"
        Background="#080C18"
        Foreground="#FFFFFF"
        FontFamily="Segoe UI"
        WindowStyle="SingleBorderWindow"
        ResizeMode="CanResize">

    <Window.Resources>
        <Style x:Key="TileStyle" TargetType="Button">
            <Setter Property="Background" Value="#14213B"/>
            <Setter Property="Foreground" Value="#FFFFFF"/>
            <Setter Property="BorderBrush" Value="#263F70"/>
            <Setter Property="BorderThickness" Value="1"/>
            <Setter Property="Padding" Value="15"/>
            <Setter Property="Margin" Value="8"/>
            <Setter Property="Cursor" Value="Hand"/>
            <Setter Property="FontSize" Value="16"/>
            <Setter Property="Template">
                <Setter.Value>
                    <ControlTemplate TargetType="Button">
                        <Border Background="{TemplateBinding Background}"
                                BorderBrush="{TemplateBinding BorderBrush}"
                                BorderThickness="{TemplateBinding BorderThickness}"
                                CornerRadius="12">
                            <ContentPresenter HorizontalAlignment="Center"
                                              VerticalAlignment="Center"/>
                        </Border>
                        <ControlTemplate.Triggers>
                            <Trigger Property="IsMouseOver" Value="True">
                                <Setter Property="Background" Value="#203A68"/>
                                <Setter Property="BorderBrush" Value="#65C8FF"/>
                            </Trigger>
                            <Trigger Property="IsPressed" Value="True">
                                <Setter Property="Background" Value="#31548D"/>
                            </Trigger>
                        </ControlTemplate.Triggers>
                    </ControlTemplate>
                </Setter.Value>
            </Setter>
        </Style>
    </Window.Resources>

    <Grid Margin="25">
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="*"/>
            <RowDefinition Height="Auto"/>
        </Grid.RowDefinitions>

        <!-- HEADER -->
        <DockPanel Grid.Row="0" Margin="5,0,5,25">
            <StackPanel DockPanel.Dock="Left">
                <TextBlock Text="NOVA"
                           FontSize="34"
                           FontWeight="Bold"
                           Foreground="#79D5FF"/>
                <TextBlock Text="GOJO INFINITY EDITION"
                           FontSize="11"
                           Foreground="#8B9DBF"
                           Margin="2,0"/>
            </StackPanel>

            <StackPanel DockPanel.Dock="Right"
                        HorizontalAlignment="Right">
                <TextBlock Text="INFINITY MODE"
                           Foreground="#A78BFA"
                           FontWeight="Bold"
                           HorizontalAlignment="Right"/>
                <TextBlock Text="WINDOWS 11"
                           Foreground="#7C91B5"
                           FontSize="11"
                           HorizontalAlignment="Right"/>
            </StackPanel>
        </DockPanel>

        <!-- HERO SECTION -->
        <Border Grid.Row="1"
                CornerRadius="18"
                Padding="30"
                Margin="0,0,0,20"
                BorderBrush="#28477C"
                BorderThickness="1">
            <Border.Background>
                <LinearGradientBrush StartPoint="0,0" EndPoint="1,1">
                    <GradientStop Color="#172C55" Offset="0"/>
                    <GradientStop Color="#10162F" Offset="0.55"/>
                    <GradientStop Color="#281747" Offset="1"/>
                </LinearGradientBrush>
            </Border.Background>

            <StackPanel>
                <TextBlock Text="WELCOME TO THE INFINITY"
                           FontSize="13"
                           Foreground="#82CFFF"
                           FontWeight="Bold"/>
                <TextBlock Text="YOUR DESKTOP. YOUR DOMAIN."
                           FontSize="29"
                           FontWeight="Bold"
                           Margin="0,8,0,5"/>
                <TextBlock Text="Enter the world of NOVA."
                           FontSize="14"
                           Foreground="#B6C8E9"/>
            </StackPanel>
        </Border>

        <!-- SEARCH -->
        <StackPanel Grid.Row="2" Margin="0,0,0,15">
            <TextBlock Text="QUICK SEARCH"
                       Foreground="#86BFFF"
                       FontWeight="Bold"
                       Margin="5,0,0,8"/>
            <TextBox x:Name="SearchBox"
                     Height="45"
                     Padding="13,9"
                     FontSize="16"
                     Background="#111D34"
                     Foreground="White"
                     BorderBrush="#36598E"
                     BorderThickness="1"
                     CaretBrush="White"/>
        </StackPanel>

        <!-- APPLICATIONS -->
        <ScrollViewer Grid.Row="3"
                      VerticalScrollBarVisibility="Auto">
            <StackPanel>
                <TextBlock Text="APPLICATIONS"
                           FontSize="17"
                           FontWeight="Bold"
                           Foreground="#8FCFFF"
                           Margin="5,0,0,10"/>

                <WrapPanel x:Name="AppPanel"/>
            </StackPanel>
        </ScrollViewer>

        <!-- FOOTER -->
        <DockPanel Grid.Row="4" Margin="5,20,5,0">
            <TextBlock Text="NOVA INFINITY  |  ANIME DESKTOP"
                       Foreground="#7086AC"
                       FontSize="11"/>
            <TextBlock x:Name="ClockText"
                       DockPanel.Dock="Right"
                       Foreground="#8BD5FF"
                       FontSize="13"
                       HorizontalAlignment="Right"/>
        </DockPanel>
    </Grid>
</Window>
'@

$reader = New-Object System.Xml.XmlNodeReader $xaml
$window = [Windows.Markup.XamlReader]::Load($reader)

$searchBox = $window.FindName("SearchBox")
$appPanel = $window.FindName("AppPanel")
$clockText = $window.FindName("ClockText")

# ==========================================
# CUSTOMIZE YOUR APPLICATIONS HERE
# ==========================================

$apps = @(
    @{Name="File Explorer"; Category="Windows"; Target="explorer.exe"},
    @{Name="Google Chrome"; Category="Browser"; Target="chrome.exe"},
    @{Name="Microsoft Edge"; Category="Browser"; Target="msedge.exe"},
    @{Name="Windows Settings"; Category="System"; Target="ms-settings:"},
    @{Name="Notepad"; Category="Windows"; Target="notepad.exe"},
    @{Name="Calculator"; Category="Windows"; Target="calc.exe"},
    @{Name="Paint"; Category="Windows"; Target="mspaint.exe"},
    @{Name="Task Manager"; Category="System"; Target="taskmgr.exe"},
    @{Name="Command Prompt"; Category="System"; Target="cmd.exe"},
    @{Name="PowerShell"; Category="System"; Target="powershell.exe"},
    @{Name="Windows Terminal"; Category="System"; Target="wt.exe"},
    @{Name="Steam"; Category="Gaming"; Target="steam.exe"},
    @{Name="Discord"; Category="Social"; Target="discord.exe"}
)

# ==========================================
# BUILD APPLICATION TILES
# ==========================================

function Build-AppTiles {
    $appPanel.Children.Clear()

    $query = $searchBox.Text.Trim().ToLowerInvariant()

    $filteredApps = @($apps | Where-Object {
        $_.Name.ToLowerInvariant().Contains($query) -or
        $_.Category.ToLowerInvariant().Contains($query)
    })

    foreach ($app in $filteredApps) {

        $localApp = $app

        $button = New-Object System.Windows.Controls.Button
        $button.Style = $window.FindResource("TileStyle")
        $button.Width = 225
        $button.Height = 105

        $stack = New-Object System.Windows.Controls.StackPanel
        $stack.HorizontalAlignment = "Center"
        $stack.VerticalAlignment = "Center"

        $name = New-Object System.Windows.Controls.TextBlock
        $name.Text = $localApp.Name
        $name.FontSize = 17
        $name.FontWeight = "SemiBold"
        $name.TextAlignment = "Center"

        $category = New-Object System.Windows.Controls.TextBlock
        $category.Text = $localApp.Category
        $category.FontSize = 11
        $category.Foreground = "#82BFFF"
        $category.TextAlignment = "Center"
        $category.Margin = "0,7,0,0"

        $stack.Children.Add($name) | Out-Null
        $stack.Children.Add($category) | Out-Null

        $button.Content = $stack

        $button.Add_Click({
            try {
                Start-Process -FilePath $localApp.Target -ErrorAction Stop
            }
            catch {
                [System.Windows.MessageBox]::Show(
                    "Could not launch $($localApp.Name).`nCheck whether it is installed.",
                    "NOVA Launcher",
                    "OK",
                    "Warning"
                ) | Out-Null
            }
        }.GetNewClosure())

        $appPanel.Children.Add($button) | Out-Null
    }

    if ($filteredApps.Count -eq 0) {
        $empty = New-Object System.Windows.Controls.TextBlock
        $empty.Text = "No applications found."
        $empty.Foreground = "#AABBDD"
        $empty.Margin = "10"
        $appPanel.Children.Add($empty) | Out-Null
    }
}

# ==========================================
# LIVE SEARCH
# ==========================================

$searchBox.Add_TextChanged({
    Build-AppTiles
})

# ==========================================
# LIVE CLOCK
# ==========================================

$timer = New-Object System.Windows.Threading.DispatcherTimer
$timer.Interval = [TimeSpan]::FromSeconds(1)

$timer.Add_Tick({
    $clockText.Text = (Get-Date).ToString("dddd, dd MMMM yyyy  |  hh:mm:ss tt")
})

$timer.Start()

# INITIALIZE
Build-AppTiles

# START LAUNCHER
$window.Add_Closed({
    $timer.Stop()
})

$null = $window.ShowDialog()
