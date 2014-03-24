#Shortcut
Shortcut allows you to quickly and easily bind system-wide hot keys to callbacks defined by your application so that when the system-wide hot key in question is pressed by the end-user, the bound callback will be invoked. 

Shortcut makes use of fluent interfaces to enable the following succinct syntax:

```c#
_hotkeyBinder.Bind(hotkeyCombination).To(HotkeyCallback);
```

##How Do You Use It?


In order to use Shortcut in your own application you must first [reference](http://msdn.microsoft.com/en-us/library/wkze6zky.aspx) the Shortcut class library. Once you have referenced the Shortcut class library, pease refer to the sample application listed below for guidance.

Alternatively, you could refer to the sample project called *[Shortcut.Demo](https://github.com/ByteBlast/Shortcut/blob/master/src/Shortcut.Demo/Forms/MainForm.cs)* that can be found in the project repository for guidance.

```c#
public partial class MainForm : Form {

    // 1. Declare the Shortcut.HotkeyBinder.
    //
    private readonly HotkeyBinder _hotkeyBinder = new HotkeyBinder();
    
    // 2. Declare the callback that you would like Shortcut to invoke when 
    // the specified system-wide hot key is pressed.
    //
    private static void HotkeyCallback() {
        MessageBox.Show("You pressed a system-wide hot key!");
    }
    
    private void MainForm_Load(object sender, System.EventArgs e) {
    
        // 3. Tell Shortcut to bind the specified system-wide hot key to the
        // callback you defined earlier. 
        //
        var hotkeyCombination = new HotkeyCombination(Modifiers.Control, Keys.F);
        _hotkeyBinder.Bind(hotkeyCombination).To(HotkeyCallback);
    
        // 4. Alternative syntax.
        //
        _hotkeyBinder.Bind(Modifiers.Control | Modifiers.Shift, Keys.A).To(HotkeyCallback);    
    }
}
```

##Documentation

Shortcut does not expose that many public members however, all of those that it does are decorated with XML comments. Some public methods that you should be aware of are as followed:

* Create a system-wide hot key binding using the `HotkeyBinder.Bind` Method. 
* Remove a binding using the `HotkeyBinder.Unbind` Method. 
* Determine whether a system-wide hot key has already been bound using `HotkeyBinder.IsHotkeyAlreadyBound`.

Contributions of any kind (issues, pull requests etc.) are encouraged :D