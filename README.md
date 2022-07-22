# Test long file path

(deutsch)[./README_de.md]

<details>
  <summary>Table of Contents</summary>

* [About](#about)
* [How to](#how-to)
  1. [Prerequisites](#prerequisites)
  2. [Configure Windows](#configure-windows)
  3. [Configure Git](#configure-git)
* [Limitations](#limitations)
* [Links](#links)
  
</details>

## About

This project describes how you can handle long file path with Git and Windows.
This is importent by default the Windows OS does not allow path names longer than 260 characters.
However, it is possible to configure the operating system to allow limited work with overlong file trees.

This project it self is an example because the relative path to the containing file `es.txt` has 265 characters.
So without configuration it is not possible to checkout this project on a Windows operating system.

[back to top](#test-long-file-path)

## How to

In this chapter I will show you how to checkout Git projects that have a file structure with paths longer than 260.

### Prerequisites

* The shown steps are tested in a Windows 10 Enterprise environment
* The tested Git client was Git for Windows
* Administrative rights for the local computer are required

### Configure Windows

1. Press the Windows key and type `gpedit`.
This opens the __Edit group police__ window.
2. Go to __Administrative Templates > System > Filesystem__ and open __Enable Win32 long paths__.
3. Select the radio option __Enabled__ and press __OK__.
4. Now press the Window key again and type `cmd`. This opend the Windows Command Prompt.
5. Type the following commands to apply the changed group policies

```
> gpupdate /target:computer /force
> gpupdate /target:user /force
```

Now you can create file with a path longer than 260 charaters the the __Command Prompt__ tool.

### Configure Git

After you have configured Windows to support long file path you also have to do the same with your local Git installation.

1. Press the Windows key and type `git bash`. When open the Git Bash use the option __Run as administrator__.
2. Type the following command

```
$ git config --system core.longpaths true
```

Now you can checkout Git projects that have deep file structure and result into paths longer than 260 character on you local system.

[back to top](#test-long-file-path)

## Limitations

The file path length problem cannot be completely solved with the above steps.
As far as I am informed, this problem is related to an older Windows API, which is why not all programs can handle files in such a deep folder structure. 

Examples of programs that do not support long file paths:
* Windows Explorer (Supports viewing only).
* Notepad++

Examples of programs that support long file paths:
* Visual Studio Code
* Notepad (Windows board tool)

[back to top](#test-long-file-path)

## Links

I personally find this article about the general problem in Windows very helpful.
 * https://helpdeskgeek.com/how-to/how-to-fix-filename-is-too-long-issue-in-windows/

Here is another Stackoverflow article about the problem in Git for Windows
 * https://stackoverflow.com/questions/22575662/filename-too-long-in-git-for-windows

 [back to top](#test-long-file-path)