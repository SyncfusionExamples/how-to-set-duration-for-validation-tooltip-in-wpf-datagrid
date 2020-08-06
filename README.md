# How to set duration for validation ToolTip in WPF DataGrid (SfDataGrid)?  

How to set duration for validation ToolTip in WPF DataGrid (SfDataGrid)?  

# About the sample

In SfDataGrid, you can change the show duration for the validation error tooltip by setting ToolTipService.ShowDuration in style of the GridCell

```xml
<Window.Resources>
    <ControlTemplate x:Key="ValidationToolTipTemplate">
        <Grid x:Name="Root" 
        Margin="5,0" 
        Opacity="0" 
        RenderTransformOrigin="0,0">
            <Grid.RenderTransform>
                <TranslateTransform x:Name="xform" X="-25" />
            </Grid.RenderTransform>
            <VisualStateManager.VisualStateGroups>
                <VisualStateGroup Name="OpenStates">
                    <VisualStateGroup.Transitions>
                        <VisualTransition GeneratedDuration="0" />
                        <VisualTransition GeneratedDuration="0:0:0.2" To="Open">
                            <Storyboard>
                                <DoubleAnimation Duration="0:0:0.2" 
                                            Storyboard.TargetName="xform" 
                                            Storyboard.TargetProperty="X" 
                                            To="0">
                                    <DoubleAnimation.EasingFunction>
                                        <BackEase Amplitude=".3" EasingMode="EaseOut" />
                                    </DoubleAnimation.EasingFunction>
                                </DoubleAnimation>
                                <DoubleAnimation Duration="0:0:0.2" 
                                            Storyboard.TargetName="Root" 
                                            Storyboard.TargetProperty="Opacity" 
                                            To="1" />
                            </Storyboard>
                        </VisualTransition>
                    </VisualStateGroup.Transitions>
                    <VisualState x:Name="Closed">
                        <Storyboard>
                            <DoubleAnimation Duration="0" 
                                        Storyboard.TargetName="Root" 
                                        Storyboard.TargetProperty="Opacity" 
                                        To="0" />
                        </Storyboard>
                    </VisualState>
                    <VisualState x:Name="Open">
                        <Storyboard>
                            <DoubleAnimation Duration="0" 
                                        Storyboard.TargetName="xform" 
                                        Storyboard.TargetProperty="X" 
                                        To="0" />
                            <DoubleAnimation Duration="0" 
                                        Storyboard.TargetName="Root" 
                                        Storyboard.TargetProperty="Opacity" 
                                        To="1" />
                        </Storyboard>
                    </VisualState>
                </VisualStateGroup>
            </VisualStateManager.VisualStateGroups>

            <Border Margin="4,4,-4,-4" 
            Background="#052A2E31" 
            CornerRadius="5" />
            <Border Margin="3,3,-3,-3" 
            Background="#152A2E31" 
            CornerRadius="4" />
            <Border Margin="2,2,-2,-2" 
            Background="#252A2E31" 
            CornerRadius="3" />
            <Border Margin="1,1,-1,-1" 
            Background="#352A2E31" 
            CornerRadius="2" />

            <Border Background="#FFDC000C" CornerRadius="2" />
            <Border CornerRadius="2">
                <TextBlock MaxWidth="250" 
                    Margin="8,4,8,4" 
                    Foreground="White" 
                    Text="{TemplateBinding Tag}" 
                    TextWrapping="Wrap" 
                    UseLayoutRounding="false" />
            </Border>
        </Grid>
    </ControlTemplate>
    <Style TargetType="syncfusion:GridCell">
        <Setter Property="Template">
            <Setter.Value>
                <ControlTemplate TargetType="syncfusion:GridCell">
                    <Grid SnapsToDevicePixels="True">
                        <VisualStateManager.VisualStateGroups>
                            <VisualStateGroup x:Name="IndicationStates">
                                <VisualState x:Name="NoError">
                                    <Storyboard BeginTime="0">
                                        <ObjectAnimationUsingKeyFrames BeginTime="00:00:00" 
                                                                Storyboard.TargetName="PART_InValidCellBorder" 
                                                                Storyboard.TargetProperty="(UIElement.Visibility)">
                                            <DiscreteObjectKeyFrame KeyTime="00:00:00" Value="{x:Static Visibility.Collapsed}" />
                                        </ObjectAnimationUsingKeyFrames>
                                    </Storyboard>
                                </VisualState>
                                <VisualState x:Name="HasError">
                                    <Storyboard>
                                        <ObjectAnimationUsingKeyFrames BeginTime="00:00:00" 
                                                                Storyboard.TargetName="PART_InValidCellBorder" 
                                                                Storyboard.TargetProperty="(UIElement.Visibility)">
                                            <DiscreteObjectKeyFrame KeyTime="00:00:00" Value="{x:Static Visibility.Visible}" />
                                        </ObjectAnimationUsingKeyFrames>
                                    </Storyboard>
                                </VisualState>
                            </VisualStateGroup>
                            <VisualStateGroup x:Name="BorderStates">
                                <VisualState x:Name="NormalCell" />
                                <VisualState x:Name="FrozenColumnCell"/>
                                <VisualState x:Name="FooterColumnCell">
                                    <Storyboard BeginTime="0">
                                        <ThicknessAnimationUsingKeyFrames BeginTime="0" 
                                                                    Duration="1" 
                                                                    Storyboard.TargetName="PART_GridCellBorder" 
                                                                    Storyboard.TargetProperty="BorderThickness">
                                            <EasingThicknessKeyFrame KeyTime="0" Value="1,0,1,1" />
                                        </ThicknessAnimationUsingKeyFrames>
                                    </Storyboard>
                                </VisualState>
                                <VisualState x:Name="BeforeFooterColumnCell">
                                    <Storyboard BeginTime="0">
                                        <ThicknessAnimationUsingKeyFrames BeginTime="0" 
                                                                    Duration="1" 
                                                                    Storyboard.TargetName="PART_GridCellBorder" 
                                                                    Storyboard.TargetProperty="BorderThickness">
                                            <EasingThicknessKeyFrame KeyTime="0" Value="0,0,0,1" />
                                        </ThicknessAnimationUsingKeyFrames>
                                    </Storyboard>
                                </VisualState>
                            </VisualStateGroup>
                        </VisualStateManager.VisualStateGroups>
                        <Border Background="{TemplateBinding CellSelectionBrush}" 
                        SnapsToDevicePixels="True" 
                        Visibility="{TemplateBinding SelectionBorderVisibility}" />

                        <Border x:Name="PART_GridCellBorder" 
                        Background="{TemplateBinding Background}" 
                        BorderBrush="{TemplateBinding BorderBrush}" 
                        BorderThickness="{TemplateBinding BorderThickness}" 
                        SnapsToDevicePixels="True">
                            <ContentPresenter Margin="{TemplateBinding Padding}" Opacity="{TemplateBinding AnimationOpacity}" />
                        </Border>

                        <Border Margin="0,0,1,1" 
                        Background="Transparent" 
                        BorderBrush="{TemplateBinding CurrentCellBorderBrush}" 
                        BorderThickness="{TemplateBinding CurrentCellBorderThickness}" 
                        IsHitTestVisible="False" 
                        SnapsToDevicePixels="True" 
                        Visibility="{TemplateBinding CurrentCellBorderVisibility}" />
                        <Border x:Name="PART_InValidCellBorder" 
                        Width="10" 
                        Height="10" 
                        HorizontalAlignment="Right" 
                        VerticalAlignment="Top" 
                        SnapsToDevicePixels="True" 
                        Visibility="Collapsed">
                            <ToolTipService.ShowDuration>
                                1000 <!--ShowDuration is set to 1000 milli seconds-->
                            </ToolTipService.ShowDuration>
                            <ToolTipService.ToolTip>
                                <ToolTip Background="#FFDB000C" 
                                    Placement="Right" 
                                     
                                    PlacementRectangle="20,0,0,0" 
                                    Tag="{TemplateBinding ErrorMessage}" 
                                    Template="{StaticResource ValidationToolTipTemplate}" />
                            </ToolTipService.ToolTip>
                            <Path Data="M0.5,0.5 L12.652698,0.5 12.652698,12.068006 z" 
                            Fill="Red" 
                            SnapsToDevicePixels="True" 
                            Stretch="Fill" />
                        </Border>
                    </Grid>
                </ControlTemplate>
            </Setter.Value>
        </Setter>
    </Style>
</Window.Resources>
```

## Requirements to run the demo
 Visual Studio 2015 and above versions
