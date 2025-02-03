Auto-taper RX.NET scanner setup

**By: Miguel Carreón**
*miguelcarreo@essilorluxottica.id*

## Setup Procedure

In the following procedure you will learn how to setup a **Zebra Symbol** Scanner to work with a usb interface in the RX.NET program.

This will utilize the open source program [**Autohotkey (AHK)**](https://www.autohotkey.com/), specifically v1.1 which you can download [here](https://www.autohotkey.com/download/ahk-install.exe).
The basic logic is that the Symbol scanner gets programmed to send an F23 keystroke (in honor to Michael Jordan), and then this keystroke detonates an AHK routine, said routine is what allows the interaction with RX.NET.

### Things you will need
- Zebra Symbol Barcode Reader (preferably DS2208 or any other with the same functions).
- [Autohotkey v1.1](https://www.autohotkey.com/download/ahk-install.exe) (it is a deprecated version but is the one that works)

### Physical Setup
1. Connect the barcode reader to the PC.

### Programming

#### Step 1

Scan the **Restore Defaults** barcode \
![Restore Defaults Barcode](https://raw.githubusercontent.com/Miguel-Carreon13/scanner-procedures/main/images/defaults.png "Restore Defaults Barcode")

#### Step 2

Scan the **Suffix 1 Data Transmission Format** barcode \
![Suffix 1 Data Transmission Format Barcode](https://raw.githubusercontent.com/Miguel-Carreon13/scanner-procedures/main/images/suffix.png "Suffix 1 Data Transmission Format Barcode")

<br>
<br>
<br>

#### Step 3

Setup the letter/number to use as prefix

To do this setup we will use the **5023** ASCII character set that represents an "F23" keystroke. To do that scann the following series of barcodes in the order they appear.

![5 Barcode](https://raw.githubusercontent.com/Miguel-Carreon13/scanner-procedures/refs/heads/main/images/5.png "5 Barcode")

![0 Barcode](https://raw.githubusercontent.com/Miguel-Carreon13/scanner-procedures/main/images/0.png "0 Barcode")

![2 Barcode](https://raw.githubusercontent.com/Miguel-Carreon13/scanner-procedures/refs/heads/main/images/2.png "2 Barcode")

![3 Barcode](https://raw.githubusercontent.com/Miguel-Carreon13/scanner-procedures/refs/heads/main/images/3.png "3 Barcode")

#### Step 4

Scan the **\<Data\>\<Suffix 1>** barcode \
![\<Data\>\<Suffix 1> Barcode](https://raw.githubusercontent.com/Miguel-Carreon13/scanner-procedures/refs/heads/main/images/suffix1.png "\<Data\>\<Suffix 1> Barcode")

#### Step 5

Scan the **Presentation (Blink)** barcode \
![Presentation (Blink) Barcode](https://raw.githubusercontent.com/Miguel-Carreon13/scanner-procedures/refs/heads/main/images/presentation.png "Presentation (Blink) Barcode")


### Keystroke Routine

In order to do a flag using the RX.NET application, a series of steps should be taken, thanks to the keyboard command interface that is built in the app, this steps can be also done via key combinations
This is what makes possible the automatization of this process.
However, the routine requires complex keystrokes and timers, that would be difficult to impossible to program in the barcode reader itself.

#### Steps to flag automatically in RX.NET:
1. Send barcode data.
1. Send ***ENTER*** keystroke (enters the data sent in step 1 in the app).
1. Wait 500 milliseconds (wait for the pop-up window to open).
1. Send letter ***O*** (acknowledges any warning or error message shown).
1. Wait 500 milliseconds.
1. Send ***Alt + S*** (saves the entered data).
1. Wait 500 milliseconds.
1. Send ***ENTER*** keystroke (closes any error or message pop-up window).

In order to make this routine possible to automate, a software called [**Autohotkey (AHK)**](https://www.autohotkey.com/) is used.
The scanner is only programmed to send an F23 key (in honor to Michael Jordan as mentioned before, also because it does not affect any app or OS native behavior), this triggers the [**AHK**](https://www.autohotkey.com/) script executing the routine.
The routine is programmed as a script, when it runs, it emulates keystrokes of an HID device.

#### AHK script:
```
SleepTime := 100  	; Declare sleep time in milliseconds
F23::			; When F23 is pressed in honor to MJ
    Send, {Enter}       ; Press Enter
    Sleep, SleepTime    ; Pause for the defined time
    Send, o             ; Press the letter 'o'
    Sleep, SleepTime    ; Pause for the defined time
    Send, !s            ; Press Alt+S (Alt is represented by !)
    Sleep, SleepTime    ; Pause for the defined time
    Send, {Enter}       ; Press Enter again
return
```

#### Steps to setup the script:
1. Install [Autohotkey v1.1](https://www.autohotkey.com/download/ahk-install.exe).
1. Copy the script into a text editor and save it as an AutoHotKey Script file using the *.ahk* extension.
1. Run the script by double-clicking it or right clicking it then pressing *Run script*.
1. Make sure the script is running in the background by checking the AHK icon in the hidden items tray in the toolbar (hovering your cursor on the icon should show the script's name).
1. Verify the correct execution of the routne after it is triggered.
