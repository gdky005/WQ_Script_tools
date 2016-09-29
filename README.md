# WQ_Script_tools
我的脚本工具：

1. windows 上的 bat 脚本命令；
2. Mac 上的脚本工具 sh 命令。


### Mac sh 的脚本代码
```
#!/usr/bin/env bash
echo "当前 sh 的命令路径是:" $0

filePath=$0

chart="/"
if [[ $filePath =~ $chart ]]; then
	parentPath=${filePath%/*}
	echo "自动跳转到 " $parentPath
	cd $parentPath
fi

parentPath=$(ls *.jar)
echo "查找到 jar 文件：" $parentPath
java -jar $parentPath
```

### Windows bat 脚本

##### install_call.bat
```
@echo %0

set a=%0
set a=%a:"=%

set myPath=%a:\install_call.bat=%
set path=%a:~0,2%



@echo %path%
@echo %myPath%



%path%
cd %myPath%\ADB_CMD
call "%myPath%\bin\install_apk.bat"
call "%myPath%\bin\install_test.bat"
call "%myPath%\bin\run_monkey.bat"

pause
```
##### install_test.bat
```
@echo %0

set a=%0
set myPath=%a:\bin\install_test.bat=%
@echo %myPath%

adb install -r %myPath%\apk\app-debug-androidTest.apk
pause
```
##### install_apk.bat
```
@echo %0

set a=%0
set myPath=%a:\bin\install_apk.bat=%
@echo %myPath%

adb install -r %myPath%\apk\app-debug.apk
pause
```

#### run_monkey.bat
```
adb shell am instrument -w -r   -e debug false -e class wq.gdky005.wx.WeiXinTest#testWeiXinAddUser wq.gdky005.wx.test/android.support.test.runner.AndroidJUnitRunner

pause
```




