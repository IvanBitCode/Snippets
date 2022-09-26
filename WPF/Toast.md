This class creates a toast notification (Android style)

```csharp
public class Toast
{
    private Window _toastWindow;
    private DispatcherTimer _timer = new DispatcherTimer();
    private DoubleAnimation _animation;

    private Toast(Window owner, string messageText)
    {
        CreateUI(owner, messageText);
    }

    private void CreateUI(Window owner, string messageText)
    {
        _toastWindow = new Window
        {
            SizeToContent = SizeToContent.WidthAndHeight,
            AllowsTransparency = true,
            WindowStyle = WindowStyle.None,
            Background = Brushes.Transparent,
            ShowInTaskbar = false,
            MaxWidth = 240,
            WindowStartupLocation = WindowStartupLocation.CenterOwner,
            Owner = owner
        };

        TextBlock message = new TextBlock
        {
            Text = messageText,
            TextWrapping = TextWrapping.Wrap,
            Foreground = Brushes.White,
            FontSize = 14
        };

        StackPanel panel = new StackPanel
        {
            Margin = new Thickness(10),
            HorizontalAlignment = HorizontalAlignment.Center,
            VerticalAlignment = VerticalAlignment.Center
        };
        panel.Children.Add(message);

        Border border = new Border
        {
            Background = new SolidColorBrush(Color.FromArgb(204, 10, 10, 10)),
            CornerRadius = new CornerRadius(10),
            Child = panel
        };

        _toastWindow.Content = border;
    }

    public static Toast Create(Window owner, string messageText)
    {
        return new Toast(owner, messageText);
    }

    public void Show(int duration)
    {
        duration--; // Substract 1 sec because in/out animations add 1 second to the toast
        if (duration <= 0 || duration > 10)
        {
            duration = 3;
        }

        _timer.Interval = TimeSpan.FromSeconds(duration);
        _timer.Tick += new EventHandler(Timer_Tick);
        _timer.Start();

        _animation = new DoubleAnimation(0.0, 1.0, TimeSpan.FromSeconds(0.5));
        _toastWindow.BeginAnimation(UIElement.OpacityProperty, _animation);

        _toastWindow.Show();
    }

    void Timer_Tick(object sender, EventArgs e)
    {
        _timer.Stop();

        _animation = new DoubleAnimation(1.0, 0.0, TimeSpan.FromSeconds(0.5));
        _animation.Completed += HideAnimation_Completed;
        _toastWindow.BeginAnimation(UIElement.OpacityProperty, _animation);
    }

    private void HideAnimation_Completed(object sender, EventArgs e)
    {
        _toastWindow.Close();
    }
}
```
