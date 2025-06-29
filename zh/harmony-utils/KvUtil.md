# harmony-utils之KvUtil，键值型数据库工具类

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

##### put  添加指定类型的键值对到数据库

```
KvUtil.put("name", "张三叁");
KvUtil.put("id", 10018);
KvUtil.put("sex", RandomUtil.getRandomBoolean());
KvUtil.put("info", RandomUtil.getRandomUint8Array(8));
```

##### get  获取指定键的值

```
 let kv1 = await KvUtil.get("name");
```

##### getString  获取指定键的值，string类型

```
 let kv2 = await KvUtil.getString('name');
```

##### getNumber  获取指定键的值，number类型

```
 let kv3 = await KvUtil.getNumber("id");
```

##### getBoolean  获取指定键的值，boolean类型

```
 let kv4 = await KvUtil.getBoolean('sex');
```

##### getUint8Array  获取指定键的值，uint8Array类型

```
 let kv5 = await KvUtil.getUint8Array('info');
```

##### delete  从数据库中删除指定键值的数据

```
KvUtil.delete("name");
ToastUtil.showToast('删除缓存成功');
```

##### putBatch  批量插入键值对到SingleKVStore数据库中

```
let entries: distributedKVStore.Entry[] = [];
for (let i = 0; i < 10; i++) {
  let key = 'batch_test_string_key';
  let entry: distributedKVStore.Entry = {
    key: key + i,
    value: {
      type: distributedKVStore.ValueType.STRING,
      value: 'batch_test_string_value'
    }
  }
  entries.push(entry);
}
KvUtil.putBatch(entries).then(() => {
  ToastUtil.showToast('批量插入成功');
}).catch((err: BusinessError) => {
  ToastUtil.showToast('批量插入异常！');
});
```

##### deleteBatch  批量删除SingleKVStore数据库中的键值对

```
let keys = ["batch_test_string_key0","batch_test_string_key1","batch_test_string_key2","batch_test_string_key3"];
KvUtil.deleteBatch(keys).then(() => {
  ToastUtil.showToast('批量删除成功');
}).catch((err: BusinessError) => {
  ToastUtil.showToast('批量删除异常！');
});
```

##### getEntries  获取匹配指定键前缀的所有键值对

```
let keyPrefix = "batch_test_string_key";
KvUtil.getEntries(keyPrefix).then((entries: distributedKVStore.Entry[]) => {
  Utils.showSheetText(JSON.stringify(entries, null, 2))
}).catch((err: BusinessError) => {
  ToastUtil.showToast(`异常信息：${err.message}`);
});
```

##### backup  以指定名称备份数据库

```
let backupFile = "BK001";
KvUtil.backup(backupFile, (err: BusinessError) => {
  if (err) {
    console.error(`Failed to backup.code is ${err.code},message is ${err.message} `);
  } else {
    console.info(`Succeeded in backupping data`);
  }
});
```

##### deleteBackup  根据指定名称删除备份文件

```
let files = ["BK001", "BK002"];
KvUtil.deleteBackup(files, (err: BusinessError, data: [string, number][]) => {
  if (err) {
    console.error(`Failed to delete Backup.code is ${err.code},message is ${err.message}`);
  } else {
    console.info(`Succeed in deleting Backup.data=${data}`);
  }
});
```

##### restore  从指定的数据库文件恢复数据库

```
let backupFile = "BK001";
KvUtil.restore(backupFile, (err: BusinessError) => {
  if (err) {
    console.error(`Failed to backup.code is ${err.code},message is ${err.message} `);
  } else {
    console.info(`Succeeded in backupping data`);
  }
});
```

##### onDataChange  订阅指定类型的数据变更通知

```
  private callBack: Callback<distributedKVStore.ChangeNotification> = (change) => {
    let pStr = JSON.stringify(change, null, 2);
    LogUtil.info(pStr);
  }
  
  KvUtil.onDataChange(distributedKVStore.SubscribeType.SUBSCRIBE_TYPE_ALL, callBack);
```

##### offDataChange  取消订阅数据变更通知

```
KvUtil.offDataChange(callBack);
ToastUtil.showToast('取消订阅数据变更通知');
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

