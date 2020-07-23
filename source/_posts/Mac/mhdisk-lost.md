我的移动硬盘有很长一段时间没用过了，连接 Mac 的时候发现无法挂载了，然后进行了多次非正常推出（直接拔 usb 接口）。以为彻底凉了，好在通过网上的方法解决了，所以记录下本次的解决办法。

1. 打开 `terminal` 工具，使用 `diskutil list` 查看宗卷列表，一般对应的是 `/dev/disk2`，如果是某个盘符无法挂载，则一般对应的是 `/dev/disk2sx`，例如 `/dev/disk2s2`
2. 卸载盘符
  - 整盘卸载 `diskutil unmountDisk /dev/disk2`
3. 挂载盘符
  - 如果整盘无法挂载，则输入 `sudo diskutil mount /dev/disk2`
  - 如果是某个盘符无法挂载，，则输入 `sudo diskutil mount /dev/disk2s2`

&emsp;&emsp;当然，挂载可能会失败，甚至出现 `timed out waiting to mount`

4. 再看下移动硬盘的灯是否一直在闪烁，如果是，那么就说明有进程一直在与硬盘进行读或写，遇到这种情况继续往下看

5. 尝试干掉 `fsck`，这个方案原文参见 [External drive does not mount after plug off without eject](https://apple.stackexchange.com/questions/235309/external-drive-does-not-mount-after-plug-off-without-eject)

<p style="padding: 0 30px">关键内容：I was having the exact same issue where unmountDisk would work fine but eject would result in the "timed out" message. I finally found a suggestion to see if fsck was holding the disk hostage. A quick ps aux | grep fsck revealed that indeed it was hijacking the disk/volume as soon as it was plugged in. sudo pkill -f fsck (or just kill with the PID if you prefer) immediately allowed the volume to be mounted. </p>

<p style="padding: 0 30px">输入 `ps aux | grep fsck`，如果存在 `fsck` 进程，运行 `sudo pkill -f fsck` 杀掉进程，再看下盘符是否可以正常退出了（或者看下移动硬盘的灯是否还在闪烁），如果正常退出了，那么就说明解决了，接下来就可以查看移动硬盘里的文件了。</p>

最后的建议：
  - 不要随意拔掉 usb 接口，移动硬盘与电脑进程交互的时候粗暴的中断可能会操作到硬盘的分区、存储，严重甚至会导致硬盘坏掉
  - 虽然此次问题解决了，但是保险起见，对移动硬盘进行下格式化，再把文件存回去
