# harmony-utils之FileUtil，文件相关工具类

## harmony-utils 简介与说明

------
[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils) 一款功能丰富且极易上手的HarmonyOS工具库，借助众多实用工具类，致力于助力开发者迅速构建鸿蒙应用。其封装的工具涵盖了APP、设备、屏幕、授权、通知、线程间通信、弹框、吐司、生物认证、用户首选项、拍照、相册、扫码、文件、日志，异常捕获、字符、字符串、数字、集合、日期、随机、base64、加密、解密、JSON等一系列的功能和操作，能够满足各种不同的开发需求。    
[picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils) 是harmony-utils拆分出来的一个子库，包含PickerUtil、PhotoHelper、ScanUtil。

下载安装  
`ohpm i @pura/harmony-utils`  
`ohpm i @pura/picker_utils`

 ```
  //全局初始化方法，在UIAbility的onCreate方法中初始化 AppUtil.init()
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    AppUtil.init(this.context);
  }
 ```

## API方法与使用

------

##### getFilesDirPath  获取文件目录下的文件夹路径或文件路径

```
let path1 = FileUtil.getFilesDirPath('');
let path2 = FileUtil.getFilesDirPath("", "TEST.txt");
let path3 = FileUtil.getFilesDirPath('download/wps/ppt', 'dev.text');
let path4 = FileUtil.getFilesDirPath("download/wps/wps");
let path5 = FileUtil.getFilesDirPath(`${getContext().filesDir}/download/apk`, "app.apk");
let path6 = FileUtil.getFilesDirPath(`${getContext().filesDir}/download/wps/ppt`);
```

##### getCacheDirPath  获取缓存目录下的文件夹路径或文件路径

```
 let path7 = FileUtil.getCacheDirPath('download/wps/ppt', 'dev_xs.text');
```

##### getTempDirPath  获取临时目录下的文件夹路径或文件路径

```
let path8 = FileUtil.getTempDirPath('download/wps/ppt', 'dev_max.text');
```

##### hasDirPath  判断是否是完整路径

```
 let hasDirPath1 = FileUtil.hasDirPath("download/wps/测试.PDF");
 let hasDirPath2 = FileUtil.hasDirPath(`${FileUtil.getFilesDirPath("download/wps", "测试文档.doc")}`);
```

##### getFileUri  通过URI或路径，获取FileUri

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
let fileUri = FileUtil.getFileUri(filePath);
```

##### getFileName  通过URI或路径，获取文件名

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
let name = FileUtil.getFileName(filePath);
```

##### getFilePath  通过URI或路径，获取文件路径

```
let uri = "file://com.tong.yuyan.utils/data/storage/el2/base/haps/entry/files/download/wps/txt/demo.txt";
let filePath = FileUtil.getFilePath(strUri);
```

##### getParentUri  通过URI或路径，获取对应文件父目录的URI

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
if (FileUtil.accessSync(filePath)) {
  let parentUri = FileUtil.getParentUri(filePath);
} else {
  ToastUtil.showToast("文件不存在，请先创建和写入");
}
```

##### getParentPath  通过URI或路径，获取对应文件父目录的路径名

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
if (FileUtil.accessSync(filePath)) {
  let parentPath = FileUtil.getParentPath(filePath);
} else {
  ToastUtil.showToast("文件不存在，请先创建和写入");
}
```

##### getUriFromPath  以同步方法获取文件URI

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
let uri = FileUtil.getUriFromPath(filePath);
```

##### getFileExtention  根据文件名获取文件后缀

```
let fileExtention = FileUtil.getFileExtention("/data/storage/el2/base/haps/entry/files/download/demo.txt");
let fileExtention2 = FileUtil.getFileExtention("妹纸.png");
```

##### getFileDirSize  获取指定文件夹下所有文件的大小或指定文件大小

```
let path = FileUtil.getFilesDirPath("");
let fileDirSize = FileUtil.getFileDirSize(path);
ToastUtil.showToast(`文件夹下所有文件的大小：${fileDirSize}`);
```

##### isFile  判断文件是否是普通文件

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
if (FileUtil.accessSync(filePath)) {
  let isFile = FileUtil.isFile(filePath);
} else {
  ToastUtil.showToast("文件不存在，请先创建和写入");
}
```

##### isDirectory  判断文件是否是目录

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
if (FileUtil.accessSync(filePath)) {
  let isDirectory = FileUtil.isDirectory(filePath);
} else {
  ToastUtil.showToast("文件不存在，请先创建和写入");
}
```

##### rename  重命名文件或文件夹

```
let path = FileUtil.getFilesDirPath("", "test_cpoy.txt");
let path2 = FileUtil.getFilesDirPath("", "test_cpoy2.txt");
if (FileUtil.accessSync(path)) {
  FileUtil.rename(path, path2);
  ToastUtil.showToast("重命名成功");
} else {
  ToastUtil.showToast("文件不存在，请先创建或拷贝 目标文件")
}
```

##### mkdir  创建目录，当recursion指定为true，可多层级创建目录

```
let filePath = FileUtil.getFilesDirPath('app/download/test/wps/txt');
FileUtil.mkdirSync(filePath);
```

##### rmdir   删除整个目录

```
let dirPath = FileUtil.getFilesDirPath("");
FileUtil.rmdir(dirPath).then(() => {
  ToastUtil.showToast("删除整个目录成功");
});
```

##### unlink  删除单个文件

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
FileUtil.unlink(filePath).then(() => {
  ToastUtil.showToast("删除单个文件成功");
}).catch((err: BusinessError) => {
  ToastUtil.showToast("删除单个文件失败！");
});
```

##### access  检查文件是否存在

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
let bl = FileUtil.accessSync(filePath);
```

##### open  打开文件，支持使用URI打开文件

```
let path = FileUtil.getFilesDirPath("", "test.txt");
let file = FileUtil.openSync(path);
```

##### read  从文件读取数据

```
let path = FileUtil.getFilesDirPath("", "test.txt");
let file = FileUtil.openSync(path);
FileUtil.writeSync(file.fd, `"HUAWEI MatePad 11.5"S 对应的API版本是多少？`)
FileUtil.closeSync(file.fd); //关闭文件
file = FileUtil.openSync(path);
let buffer: ArrayBuffer = new ArrayBuffer(180);
FileUtil.readSync(file.fd, buffer);
let bufferStr = StrUtil.bufferToStr(buffer);
FileUtil.closeSync(file.fd); //关闭文件
```

##### readText  基于文本方式读取文件（即直接读取文件的文本内容）

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
if (FileUtil.accessSync(filePath)) {
  let txt = FileUtil.readTextSync(filePath);
  LogUtil.info(txt);
} else {
  ToastUtil.showToast("文件不存在，请先创建和写入")
}
```

##### write  将数据写入文件

```
let path = FileUtil.getFilesDirPath("", "test.txt");
let file = FileUtil.openSync(path);
FileUtil.writeSync(file.fd, `"HUAWEI MatePad 11.5"S 对应的API版本是多少？`)
FileUtil.closeSync(file.fd); //关闭文件
```

##### writeEasy  将数据写入文件，并关闭文件

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
FileUtil.writeEasy(filePath, "harmony-utils 一款高效的OpenHarmony/HarmonyOS工具包。帮助开发者快速构建鸿蒙应用。");            
```

##### close  关闭文件

```
let path = FileUtil.getFilesDirPath("", "test.txt");
let file = FileUtil.openSync(path);
FileUtil.closeSync(file.fd); //关闭文件
```

##### stat  获取文件详细属性信息

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
if (FileUtil.accessSync(filePath)) {
  let stat = FileUtil.statSyncfilePath);
  let jsonStr = `${stat.ino} - ${stat.mode} - ${stat.uid} - ${stat.gid} - ${stat.size} - ${stat.atime} - ${stat.mtime} - ${stat.isDirectory()} - ${stat.isFile()}`;
  LogUtil.info(jsonStr);
} else {
  ToastUtil.showToast("文件不存在，请先创建和写入 目标文件")
}
```

##### listFile  列出文件夹下所有文件名，支持递归列出所有文件名（包含子目录下），支持文件过滤

```
let dirPath = FileUtil.getFilesDirPath("");
let listFile = FileUtil.listFileSync(dirPath, { recursion: true });
let listFileStr = listFile.join('\n');
```

##### copyFile  复制文件

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt')
let path = FileUtil.getFilesDirPath("download/wps", "test_cpoy.txt");
if (FileUtil.accessSync(filePath)) {
  FileUtil.copyFile(filePath, path).then(() => {
    let size = FileUtil.lstatSync(path).size;
    ToastUtil.showToast("文件拷贝成功：" + size);
  })
} else {
  ToastUtil.showToast("文件不存在，请先创建和写入 目标文件");
}
```

##### copy  拷贝文件或者目录，支持拷贝进度监听

```
let path = FileUtil.getFilesDirPath("download");
let path2 = FileUtil.getFilesDirPath("copy目录");
if (FileUtil.accessSync(path)) {
  let progressListener: fs.ProgressListener = (progress: fs.Progress) => {
    LogUtil.info(`progressSize: ${progress.processedSize}, totalSize: ${progress.totalSize}`);
  };
  FileUtil.copy(FileUtil.getUriFromPath(path), FileUtil.getUriFromPath(path2),
    { "progressListener": progressListener }).then(() => {
    let size = FileUtil.lstatSync(path2).size;
    ToastUtil.showToast("文件夹拷贝成功：" + size);
  }).catch((err: BusinessError) => {
    ToastUtil.showToast("文件夹拷贝异常：" + err.message);
  })
} else {
  ToastUtil.showToast("文件夹不存在，请先创建");
}
```

##### copyDir 复制源文件夹至目标路径下，只能复制沙箱里的文件夹

```
let path = FileUtil.getFilesDirPath("download");
let path2 = FileUtil.getFilesDirPath("copyDir目录");
if (FileUtil.accessSync(path)) {
  FileUtil.copyDir(path, path2).then(() => {
    let size = FileUtil.lstatSync(path2).size;
    ToastUtil.showToast("文件夹拷贝成功：" + size);
  }).catch((err: BusinessError) => {
    ToastUtil.showToast("文件夹拷贝异常：" + err.message);
  })
} else {
  ToastUtil.showToast("文件夹不存在，请先创建");
}
```

##### moveFile  移动文件

```
let path = FileUtil.getFilesDirPath("download/wps", "test_cpoy.txt");
let path2 = FileUtil.getFilesDirPath("download/txt", "test_cpoy.txt");
if (FileUtil.accessSync(path)) {
  FileUtil.moveFile(path, path2).then(() => {
    ToastUtil.showToast("移动文件成功");
  })
} else {
  ToastUtil.showToast("文件不存在")
}
```

##### moveDir  移动源文件夹至目标路径下

```
let path = FileUtil.getFilesDirPath("copyDir目录");
let path2 = FileUtil.getFilesDirPath("moveDir目录");
if (FileUtil.accessSync(path)) {
  FileUtil.moveDir(path, path2).then(() => {
    ToastUtil.showToast("文件夹移动成功");
  }).catch((err: BusinessError) => {
    ToastUtil.showToast("文件夹移动异常：" + err.message);
  })
} else {
  ToastUtil.showToast("文件夹不存在，请先创建");
}
```

##### truncate  截断文件

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
FileUtil.truncate(filePath, 15);
```

##### lstat  获取链接文件信息

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
let stat = FileUtil.lstatSync(filePath);
let jsonStr = `${stat.ino} - ${stat.mode} - ${stat.uid} - ${stat.gid} - ${stat.size} - ${stat.atime} - ${stat.mtime} - ${stat.isDirectory()} - ${stat.isFile()}`;
LogUtil.info(jsonStr);
```

##### fsync  同步文件数据

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
let file = fs.openSync(filePath);
FileUtil.fsync(file.fd).then(() => {
  LogUtil.info("同步成功！");
}).catch((err: BusinessError) => {
  LogUtil.error("同步失败， error信息: " + err.message + ", error code: " + err.code);
}).finally(() => {
  FileUtil.closeSync(file);
});
```

##### fdatasync  实现文件内容数据同步

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
let file = FileUtil.openSync(filePath);
FileUtil.fdatasync(file.fd).then(() => {
  LogUtil.info("sync data succeed");
}).catch((err: BusinessError) => {
  LogUtil.error("sync data failed with error message: " + err.message + ", error code: " + err.code);
}).finally(() => {
  FileUtil.closeSync(file);
});
```

##### createStream  基于文件路径打开文件流

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
FileUtil.createStream(filePath, "a+").then((stream: fs.Stream) => {
  stream.closeSync();
  LogUtil.info("createStream succeed");
}).catch((err: BusinessError) => {
  LogUtil.error("createStream failed with error message: " + err.message + ", error code: " + err.code);
});
```

##### fdopenStream  基于文件描述符打开文件流

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
let file = FileUtil.openSync(filePath);
FileUtil.fdopenStream(file.fd, "r+").then((stream: fs.Stream) => {
  console.info("openStream succeed");
  stream.closeSync();
}).catch((err: BusinessError) => {
  console.error("openStream failed with error message: " + err.message + ", error code: " + err.code);
  fs.closeSync(file); //文件流打开失败后，文件描述符需要手动关闭
});
```

##### mkdtemp  创建临时目录

```
let path = FileUtil.getFilesDirPath() + "/临时目录/download/temp";
let tempPath = FileUtil.mkdtempSync(path);
ToastUtil.showToast("操作成功: " + tempPath);
```

##### dup  将文件描述符转化为File

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
let file = FileUtil.openSync(filePath, fs.OpenMode.READ_WRITE);
let fd: number = file.fd;
let file2 = FileUtil.dup(fd);
LogUtil.info("The name of the file2 is " + file2.name);
FileUtil.closeSync(file);
FileUtil.closeSync(file2);
```

##### utimes  修改文件最近访问时间属性

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo_time.txt');
let file = FileUtil.openSync(filePath, fs.OpenMode.READ_WRITE);
FileUtil.writeSync(file.fd, "harmony-utils一款高效的OpenHarmony/HarmonyOS工具包。帮助开发者快速构建鸿蒙应用！");
FileUtil.closeSync(file);
FileUtil.utimes(filePath, new Date().getTime());
```

##### getFormatFileSize  格式化文件大小

```
let sizeStr = FileUtil.getFormatFileSize(1020450901);
ToastUtil.showToast(`文件大小：${sizeStr}`);
```

##### checkPersistentPermission  校验所选择的多个文件或目录URI持久化授权。（需要权限：ohos.permission.FILE_ACCESS_PERSIST）

```
//cacheUri 见使用案例源码
if (StrUtil.isNotEmpty(this.cacheUri)) {
  let policie: fileShare.PolicyInfo = {
    uri: this.cacheUri,
    operationMode: fileShare.OperationMode.READ_MODE | fileShare.OperationMode.WRITE_MODE
  }
  FileUtil.checkPersistentPermission([policie]).then(() => {
    this.jsonStr = `检查权限，成功！\n${this.cacheUri}`;
  }).catch((err: BusinessError) => {
    this.jsonStr = `检查权限，异常：\n${JSON.stringify(err)}`;
  });
} else {
  ToastUtil.showToast("请先调用saveDocument()保存文件，在操作！");
}
```

##### persistPermission  对所选择的多个文件或目录URI持久化授权。（需要权限：ohos.permission.FILE_ACCESS_PERSIST）

```
//cacheUri 见使用案例源码
if (StrUtil.isNotEmpty(this.cacheUri)) {
  FileUtil.persistPermissionEasy([this.cacheUri]).then(() => {
    this.jsonStr = `授权，已授权！\n${this.cacheUri}`;
    let file = FileUtil.openSync(this.cacheUri); //uri是否可用，读取文件
    this.jsonStr = this.jsonStr + `\n\n文件名：${file.name}`;
    LogUtil.error("file: " + file.name);
  }).catch((err: BusinessError) => {
    this.jsonStr = `授权，异常：\n${JSON.stringify(err)}`;
  });
} else {
  ToastUtil.showToast("请先调用saveDocument()保存文件，在操作！");
}
```

##### revokePermission   对所选择的多个文件或目录uri取消持久化授权。（需要权限：ohos.permission.FILE_ACCESS_PERSIST）

```
//cacheUri 见使用案例源码
if (StrUtil.isNotEmpty(this.cacheUri)) {
  FileUtil.revokePermissionEasy([this.cacheUri]).then(() => {
    this.jsonStr = `移除授权，成功！`;
    let file = FileUtil.openSync(this.cacheUri); //uri是否可用，读取文件
    this.jsonStr = this.jsonStr + `\n\n文件名：${file.name}`;
    LogUtil.error("file: " + file.name);
  }).catch((err: BusinessError) => {
    this.jsonStr = `移除授权，异常：\n${JSON.stringify(err)}`;
  });
} else {
  ToastUtil.showToast("请先调用saveDocument()保存文件，在操作！");
}
```

##### activatePermission  对已经持久化授权的权限进行使能操作，否则已经持久化授权的权限仍存在不能使用的情况。（需要权限：ohos.permission.FILE_ACCESS_PERSIST）

```
//cacheUri 见使用案例源码
if (StrUtil.isNotEmpty(this.cacheUri)) {
  FileUtil.activatePermissionEasy([this.cacheUri]).then(() => {
    this.jsonStr = `使能操作，成功！\n${this.cacheUri}`;
  }).catch((err: BusinessError) => {
    this.jsonStr = `使能操作，异常：\n${JSON.stringify(err)}`;
  })
} else {
  ToastUtil.showToast("请先调用saveDocument()保存文件，在操作！");
}
```

##### deactivatePermission  取消使能授权过的多个文件或目录。（需要权限：ohos.permission.FILE_ACCESS_PERSIST）

```
//cacheUri 见使用案例源码
if (StrUtil.isNotEmpty(this.cacheUri)) {
  FileUtil.deactivatePermissionEasy([this.cacheUri]).then(() => {
    this.jsonStr = `取消使能授权，成功！\n${this.cacheUri}`;
  }).catch((err: BusinessError) => {
    this.jsonStr = `取消使能授权，异常：\n${JSON.stringify(err)}`;
  })
} else {
  ToastUtil.showToast("请先调用saveDocument()保存文件，在操作！");
}
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



