# Harmony-utils FileUtil, file-related tool class

## Introduction and description of harmony-utils

------
[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)A HarmonyOS tool library with rich features and extremely easy to use, with the help of many practical tools, is committed to helping developers quickly build Hongmeng applications. Its encapsulated tools cover APP, device, screen, authorization, notification, inter-thread communication, pop-up frames, toast, biometric authentication, user preferences, taking photos, albums, scanning codes, files, logs, exception capture, characters, strings, numbers, collections, dates, random, base64, encryption, decryption, JSON and other functions, which can meet various development needs.
[picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils)It is a sub-store split by harmony-utils, including PickerUtil, PhotoHelper, and ScanUtil.

Download and install
`ohpm i @pura/harmony-utils`  
`ohpm i @pura/picker_utils`

 ```
  //全局初始化方法，在UIAbility的onCreate方法中初始化 AppUtil.init()
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    AppUtil.init(this.context);
  }
 ```

## API methods and usage

------

##### getFilesDirPath Gets the folder path or file path in the file directory

```
let path1 = FileUtil.getFilesDirPath('');
let path2 = FileUtil.getFilesDirPath("", "TEST.txt");
let path3 = FileUtil.getFilesDirPath('download/wps/ppt', 'dev.text');
let path4 = FileUtil.getFilesDirPath("download/wps/wps");
let path5 = FileUtil.getFilesDirPath(`${getContext().filesDir}/download/apk`, "app.apk");
let path6 = FileUtil.getFilesDirPath(`${getContext().filesDir}/download/wps/ppt`);
```

##### getCacheDirPath Gets the folder path or file path in the cache directory

```
 let path7 = FileUtil.getCacheDirPath('download/wps/ppt', 'dev_xs.text');
```

##### getTempDirPath Gets the folder path or file path in the temporary directory

```
let path8 = FileUtil.getTempDirPath('download/wps/ppt', 'dev_max.text');
```

##### hasDirPath determines whether it is the complete path

```
 let hasDirPath1 = FileUtil.hasDirPath("download/wps/测试.PDF");
 let hasDirPath2 = FileUtil.hasDirPath(`${FileUtil.getFilesDirPath("download/wps", "测试文档.doc")}`);
```

##### getFileUri Get FileUri via URI or path

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
let fileUri = FileUtil.getFileUri(filePath);
```

##### getFileName Get filename via URI or path

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
let name = FileUtil.getFileName(filePath);
```

##### getFilePath gets the file path through URI or path

```
let uri = "file://com.tong.yuyan.utils/data/storage/el2/base/haps/entry/files/download/wps/txt/demo.txt";
let filePath = FileUtil.getFilePath(strUri);
```

##### getParentUri Get the URI of the corresponding file parent directory through the URI or path

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
if (FileUtil.accessSync(filePath)) {
  let parentUri = FileUtil.getParentUri(filePath);
} else {
  ToastUtil.showToast("文件不存在，请先创建和写入");
}
```

##### getParentPath Get the path name of the corresponding file parent directory through URI or path

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
if (FileUtil.accessSync(filePath)) {
  let parentPath = FileUtil.getParentPath(filePath);
} else {
  ToastUtil.showToast("文件不存在，请先创建和写入");
}
```

##### getUriFromPath Gets the file URI in a synchronous way

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
let uri = FileUtil.getUriFromPath(filePath);
```

##### getFileExtention Get file suffix based on file name

```
let fileExtention = FileUtil.getFileExtention("/data/storage/el2/base/haps/entry/files/download/demo.txt");
let fileExtention2 = FileUtil.getFileExtention("妹纸.png");
```

##### getFileDirSize Gets the size of all files in the specified folder or the specified file size

```
let path = FileUtil.getFilesDirPath("");
let fileDirSize = FileUtil.getFileDirSize(path);
ToastUtil.showToast(`文件夹下所有文件的大小：${fileDirSize}`);
```

##### isFile determines whether the file is a normal file

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
if (FileUtil.accessSync(filePath)) {
  let isFile = FileUtil.isFile(filePath);
} else {
  ToastUtil.showToast("文件不存在，请先创建和写入");
}
```

##### isDirectory determines whether the file is a directory

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
if (FileUtil.accessSync(filePath)) {
  let isDirectory = FileUtil.isDirectory(filePath);
} else {
  ToastUtil.showToast("文件不存在，请先创建和写入");
}
```

##### rename rename file or folder

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

##### mkdir creates a directory. When recursion is specified as true, you can create a directory at multiple levels

```
let filePath = FileUtil.getFilesDirPath('app/download/test/wps/txt');
FileUtil.mkdirSync(filePath);
```

##### rmdir delete the entire directory

```
let dirPath = FileUtil.getFilesDirPath("");
FileUtil.rmdir(dirPath).then(() => {
  ToastUtil.showToast("删除整个目录成功");
});
```

##### unlink Delete a single file

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
FileUtil.unlink(filePath).then(() => {
  ToastUtil.showToast("删除单个文件成功");
}).catch((err: BusinessError) => {
  ToastUtil.showToast("删除单个文件失败！");
});
```

##### access Check whether the file exists

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
let bl = FileUtil.accessSync(filePath);
```

##### open to open files, support using URI to open files

```
let path = FileUtil.getFilesDirPath("", "test.txt");
let file = FileUtil.openSync(path);
```

##### read read data from file

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

##### readText reads a file based on text (that is, directly reads the text content of the file)

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
if (FileUtil.accessSync(filePath)) {
  let txt = FileUtil.readTextSync(filePath);
  LogUtil.info(txt);
} else {
  ToastUtil.showToast("文件不存在，请先创建和写入")
}
```

##### write write write data to file

```
let path = FileUtil.getFilesDirPath("", "test.txt");
let file = FileUtil.openSync(path);
FileUtil.writeSync(file.fd, `"HUAWEI MatePad 11.5"S 对应的API版本是多少？`)
FileUtil.closeSync(file.fd); //关闭文件
```

##### writeEasy Write data to a file and close the file

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
FileUtil.writeEasy(filePath, "harmony-utils 一款高效的OpenHarmony/HarmonyOS工具包。帮助开发者快速构建鸿蒙应用。");            
```

##### close Close the file

```
let path = FileUtil.getFilesDirPath("", "test.txt");
let file = FileUtil.openSync(path);
FileUtil.closeSync(file.fd); //关闭文件
```

##### stat Get detailed file attribute information

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

##### listFile lists all file names in folders, supports recursive listing of all file names (including subdirectories), supports file filtering

```
let dirPath = FileUtil.getFilesDirPath("");
let listFile = FileUtil.listFileSync(dirPath, { recursion: true });
let listFileStr = listFile.join('\n');
```

##### copyFile Copy files

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

##### copy copy files or directories, supports copy progress monitoring

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

##### copyDir copy the source folder to the destination path, and only the folders in the sandbox can be copied.

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

##### moveFile Move file

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

##### moveDir move source folder to destination path

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

##### truncate truncate file

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
FileUtil.truncate(filePath, 15);
```

##### lstat Get link file information

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
let stat = FileUtil.lstatSync(filePath);
let jsonStr = `${stat.ino} - ${stat.mode} - ${stat.uid} - ${stat.gid} - ${stat.size} - ${stat.atime} - ${stat.mtime} - ${stat.isDirectory()} - ${stat.isFile()}`;
LogUtil.info(jsonStr);
```

##### fsync synchronizes file data

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

##### fdatasync implements file content data synchronization

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

##### createStream Open file stream based on file path

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
FileUtil.createStream(filePath, "a+").then((stream: fs.Stream) => {
  stream.closeSync();
  LogUtil.info("createStream succeed");
}).catch((err: BusinessError) => {
  LogUtil.error("createStream failed with error message: " + err.message + ", error code: " + err.code);
});
```

##### fdopenStream Open file stream based on file descriptor

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

##### mkdtemp creates temporary directory

```
let path = FileUtil.getFilesDirPath() + "/临时目录/download/temp";
let tempPath = FileUtil.mkdtempSync(path);
ToastUtil.showToast("操作成功: " + tempPath);
```

##### dup converts file descriptors to File

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo.txt');
let file = FileUtil.openSync(filePath, fs.OpenMode.READ_WRITE);
let fd: number = file.fd;
let file2 = FileUtil.dup(fd);
LogUtil.info("The name of the file2 is " + file2.name);
FileUtil.closeSync(file);
FileUtil.closeSync(file2);
```

##### utimes Modify the file's latest access time attribute

```
let filePath = FileUtil.getFilesDirPath('download/wps/txt', 'demo_time.txt');
let file = FileUtil.openSync(filePath, fs.OpenMode.READ_WRITE);
FileUtil.writeSync(file.fd, "harmony-utils一款高效的OpenHarmony/HarmonyOS工具包。帮助开发者快速构建鸿蒙应用！");
FileUtil.closeSync(file);
FileUtil.utimes(filePath, new Date().getTime());
```

##### getFormatFileSize format file size

```
let sizeStr = FileUtil.getFormatFileSize(1020450901);
ToastUtil.showToast(`文件大小：${sizeStr}`);
```

##### checkPersistentPermission Verify multiple file or directory URI persistence authorization selected. (Permission required: ohos.permission.FILE_ACCESS_PERSIST)

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

##### persistPermission Persistence authorization for multiple selected files or directory URIs. (Permission required: ohos.permission.FILE_ACCESS_PERSIST)

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

##### revokePermission Unpersistence authorization for multiple selected files or directories uri. (Permission required: ohos.permission.FILE_ACCESS_PERSIST)

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

##### activatePermission enables permissions that have been persisted authorized, otherwise permissions that have been persisted authorized cannot be used. (Permission required: ohos.permission.FILE_ACCESS_PERSIST)

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

##### deactivatePermission Cancels the enablement of multiple authorized files or directories. (Permission required: ohos.permission.FILE_ACCESS_PERSIST)

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

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



