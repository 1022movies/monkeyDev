# Xcode 14安装MonkeyDev

### <font color=red>不要使用官网的安装脚本安装，该脚本只支持到Xcode11版本</font>

### 安装方法

1. `git clone https://github.com/AloneMonkey/MonkeyDev.git`下载MonkeyDev源码

2. `git clone -b 3.x https://github.com/AloneMonkey/frida-ios-dump.git`下载frida-ios-dump源码

3.  

   ```shell
   cd MonkeyDev/bin
   sudo ./md-install
   ```

   如果报错

   ```
   curl: (7) Failed to connect to raw.githubusercontent.com port 443: Connection refused
   Failed to download raw.githubusercontent.com/AloneMonkey… to /opt/MonkeyDev/bin/dump.py
   ```

   这时候手动拷贝文件frida-ios-dump/dump.py和frida-ios-dump/dump.js，粘贴到opt/MonkeyDev/bin，并赋予权限`chmod +x /opt/MonkeyDev/bin/dump.py`;

4. 终端执行

   ```shell
   mini@minideMac-mini ~ % cd /Applications/Xcode.app/Contents
   mini@minideMac-mini Contents % find . -name Embedded-Device.xcspec
   ./PlugIns/XCBSpecifications.ideplugin/Contents/Resources/Embedded-Device.xcspec
   mini@minideMac-mini Contents % cp ./PlugIns/XCBSpecifications.ideplugin ./PlugIns/IDEiOSSupportCore.ideplugin
   ```

   如果不执行会报错

   ```shell
   File /Applications/Xcode.app/Contents/PlugIns/IDEiOSSupportCore.ideplugin/Contents/Resources/Embedded-Device.xcspec not found
   ```

   Xcode13 中没有`IDEiOSSupportCore.ideplugin`文件，`Embedded-Device.xcspec`被放在`XCBSpecifications.ideplugin`文件内，复制`IDEiOSSupportCore.ideplugin`文件，重命名为`IDEiOSSupportCore.ideplugin`

5. 打开MonkeyDev/bin/md-install执行文件，注释掉下载代码，保存(309行)

   ```shell
   #下载一些基础文件和模板文件
   #downloadGithubTarball "https://codeload.github.com/AloneMonkey/MonkeyDev/tar.gz/$branch" "$MonkeyDevPath" "MonkeyDev base"
   #downloadGithubTarball "https://codeload.github.com/AloneMonkey/MonkeyDev-Xcode-Templates/tar.gz/$branch" "$MonkeyDevPath/templates" "Xcode templates"
   
   #下载frida-ios-dump
   #echo "Downloading frida-ios-dump from Github..."
   #downloadFile "https://raw.githubusercontent.com/AloneMonkey/frida-ios-dump/3.x/dump.py" "$MonkeyDevPath/bin/dump.py"
   #downloadFile "https://raw.githubusercontent.com/AloneMonkey/frida-ios-dump/3.x/dump.js" "$MonkeyDevPath/bin/dump.js"
   
   #chmod +x "$MonkeyDevPath/bin/dump.py"
   
   ```

6. 再次执行再次执行MonkeyDev/bin/md-install，会报错

   ```
   /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/Library/Xcode/Specifications/MacOSX Package Types.xcspec not found
   ```

   Xcode13中没有这个文件，需要从老版本中复制过来，[下载地址](https://github.com/1022movies/monkeyDev)

7. 将下载下来的`Specifications`目录，放到以上路径下，重新执行MonkeyDev/bin/md-install。

8. 完成

