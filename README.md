# 等一下，好像有bug要紧急修复一下

# sUdoAC

利用计划任务，不弹出 UAC 对话框，以管理员身份带参数运行指定文件。

附带一个 sudo 命令，功能相同。

脚本不会释放任何临时文件，所有内含 vbs、powershell 代码直接执行，所有操作（创建计划任务、“安装” sudo 插件）均可以无痕卸载。

但是，要运行某个程序时，需要在 Temp 创建一个名为 ~sUdoAC_task<编号>.TMP 的临时文件，一般情况下会自动删除。

## 使用方法

双击运行管理器 sudoac.cmd，并允许管理员权限。

创建计划任务

（可选）安装 sudo 插件

然后可以使用两种方式（N 文件选择器、M 拖入窗口。文件选择器不能选中快捷方式本身，所以如果要读取快捷方式文件需要拖入窗口）创建管理员身份运行的快捷方式。

也可以直接把文件、快捷方式拖到 sudoac.cmd 上自动创建管理员权限快捷方式。（但是不会自动退出）

由于计划任务直接内置一个脚本，可以随意移动所有程序文件（如 sudoac.cmd）甚至是直接删除这些文件，快捷方式依然能正确运行。

## 注意事项

这个脚本只是实验性的，可能包含程序问题和安全隐患。

#### 已知的问题

由于使用 vbs shellexcute，sudo 命令也不支持在当前窗口执行命令，而是运行了一个新的程序。如果需要以管理员权限执行 cmd 命令，请 sudo cmd 然后在新的 cmd 窗口运行。

sudo 插件支持获取管道输入（参数 -p），但是没有管道输入时这么做会卡住。

为保证运行速度，sudo 命令脚本不会检查是否配置了计划任务，而会直接尝试运行计划任务。请自行确保计划任务存在再开始使用，否则要启动的程序任务将堆积，在下一次运行计划任务时批量运行，导致计算机卡顿。

如果原文件名过长或快捷方式参数过长，vbs 代码会拒绝执行，导致创建快捷方式的参数写不进去。这问题好像挺频繁的。可以手动把快捷方式改为指向 sudo <程序+参数> ，即换成用 sudo 插件运行这个程序来临时解决。

如果 ~sUdoAC_task<编号>.TMP 文件是空的，计划任务错误地不会删除，可能需要手动删除。

遇到一些特殊符号，sudoac.cmd 和 sudo.cmd 可能会因转义不恰当而出错。

#### 优点

虽然创建快捷方式的功能可能 bug 一堆，但 sudo 插件还是挺好用的。

## 感谢使用 :)
