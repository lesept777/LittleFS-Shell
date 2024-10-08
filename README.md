# LittleFS_Shell Command Interface Documentation

The LittleFSShell command interface provides a set of commands for interacting with the LittleFS (SPI Flash File System) on an ESP8266 or ESP32 microcontroller. The LittleFSShell class encapsulates the functionality and provides a command-line interface over the Serial port.

This is an adaptation of the original work of **masaad01** which is available here: https://github.com/masaad01/SPIFFS_Shell for SPIFFS. All credit goes to him.

## Getting Started

To use the LittleFSShell command interface, just include the header file <LittleFS_Shell.h>. The Library automatically includes the necessary files, initializes the LittleFS and starts the command interface.

```cpp
#include <LittleFS_Shell.h>

void setup() {
  // Main program setup
}

void loop() {
  // Main program loop
}
```

## Available Commands

The LittleFSShell command interface supports the following commands:

### ls \<directory\>

List the contents of a directory. The `directory` parameter is optional. If no directory is specified, the root directory will be listed.

Example usage:

```
LittleFS# ls
Name                                     Type       Size
/dir1                                    <DIR>        
file1.txt                                FILE       1234
```

### cat \<file\>

Read the contents of a file and print them to the Serial port.

Example usage:

```
LittleFS# cat file1.txt
This is the content of file1.txt.
```


### dump \<file\>

Read the contents of a file and print them to the Serial port as hexadecimal.

Example usage:

```
LittleFS# dump file2.txt
 0x22 0x48 0x65 0x6C 0x6C 0x6F 0x2C 0x57 0x6F 0x72 0x6C 0x64 0x21 0x22          	"Hello,World!"
```

### echo \<message\> \<file\>

Write a message to a file. If the file does not exist, it will be created. If the file already exists, the message will overwrite the existing content.

Example usage:

```
LittleFS# echo "Hello, World!" file2.txt
```

### append \<message\> \<file\>

Append a message to the end of a file. If the file does not exist, it will be created.

Example usage:

```
LittleFS# append "Additional content" file2.txt
```

### mv \<old\> \<new\>

Rename a file. The `old` parameter specifies the current name of the file, and the `new` parameter specifies the new name.

Example usage:

```
LittleFS# mv file1.txt newname.txt
```

### rm \<file\>

Delete a file.

Example usage:

```
LittleFS# rm file2.txt
```

### du

Print the total size of the LittleFS flash memory in kilobytes.

Example usage:

```
LittleFS# du
Flash memory size: 5120 KB
```

### df

Print the amount of used flash memory in kilobytes.

Example usage:

```
LittleFS# df
Flash memory used: 1024 KB
```

### editor \<file\>

Enter a text editor mode for appending text to a file. The `file` parameter specifies the name of the file to edit. In the text editor mode, you can enter text that will be appended to the file. Type `%exit` to exit the text editor.

Example usage:

```
LittleFS# editor file2.txt
- Text editor started. Enter text (or type '%exit' to quit, '%help' for commands):
This is some additional text.
%exit
- Text editor exited
```

### help

Show a list of available commands.

Example usage:

```
LittleFS# help
Available commands:
ls <directory> - List the contents of a directory
cat <file> - Read the contents of a file
dump <file> - Dumps the contents of a file as hexadecimal
echo <message> <file> - Write a message to a file
append <message> <file> -

 Append a message to a file
mv <old> <new> - Rename a file
rm <file> - Delete a file
du - Print total flash memory size
df - Print used flash memory
editor <file> - Enter a text editor for appending text to a file (type '%exit' to quit, '%help' for commands)
help - Show available commands
```

## Notes

- The LittleFS file system must be successfully mounted for the LittleFSShell class to function properly. If mounting fails, an error message will be printed, and the command interface will not start.
- The LittleFS_Shell.h library is still in the works, and so far, I've only had the chance to test it on the Heltec ESP32 board. If you happen to come across any problems, please don't hesitate to submit an issue report (or even better, a pull request if you're up for it!). Your feedback would be greatly appreciated!

## Limitations

- The LittleFS_Shell command interface does not support files with names containing spaces.
- LittleFS does not support folders or directory structures. All files are stored in the root directory.
- The maximum length of a LittleFS file name, including the file extension, is 30 characters. This limitation is due to the underlying file system implementation.
- The total number of files that can be stored in LittleFS is limited by the available space in the flash memory. The exact number depends on the size of the files and the available free space.
- The maximum file size that can be stored in LittleFS depends on the configuration and the SPI flash size of your microcontroller. For example, on the ESP8266, the default configuration allows a maximum file size of 64KB.
