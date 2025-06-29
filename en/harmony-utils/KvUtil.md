# Harmony-utils KvUtil, key-value database tool class

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

##### put Add key-value pairs of the specified type to the database

```
KvUtil.put("name", "张三叁");
KvUtil.put("id", 10018);
KvUtil.put("sex", RandomUtil.getRandomBoolean());
KvUtil.put("info", RandomUtil.getRandomUint8Array(8));
```

##### get get the value of the specified key

```
 let kv1 = await KvUtil.get("name");
```

##### getString Gets the value of the specified key, string type

```
 let kv2 = await KvUtil.getString('name');
```

##### getNumber Gets the value of the specified key, number type

```
 let kv3 = await KvUtil.getNumber("id");
```

##### getBoolean Gets the value of the specified key, boolean type

```
 let kv4 = await KvUtil.getBoolean('sex');
```

##### getUint8Array Gets the value of the specified key, uint8Array type

```
 let kv5 = await KvUtil.getUint8Array('info');
```

##### delete delete data with specified key value from the database

```
KvUtil.delete("name");
ToastUtil.showToast('删除缓存成功');
```

##### putBatch Insert key-value pairs in SingleKVStore database in batches

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

##### deleteBatch deletes key-value pairs in SingleKVStore database in batches

```
let keys = ["batch_test_string_key0","batch_test_string_key1","batch_test_string_key2","batch_test_string_key3"];
KvUtil.deleteBatch(keys).then(() => {
  ToastUtil.showToast('批量删除成功');
}).catch((err: BusinessError) => {
  ToastUtil.showToast('批量删除异常！');
});
```

##### getEntries Get all key-value pairs that match the specified key prefix

```
let keyPrefix = "batch_test_string_key";
KvUtil.getEntries(keyPrefix).then((entries: distributedKVStore.Entry[]) => {
  Utils.showSheetText(JSON.stringify(entries, null, 2))
}).catch((err: BusinessError) => {
  ToastUtil.showToast(`异常信息：${err.message}`);
});
```

##### backup backup database with a specified name

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

##### deleteBackup deletes backup file according to the specified name

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

##### restore restore database from specified database file

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

##### onDataChange Subscribe to data change notifications of specified types

```
  private callBack: Callback<distributedKVStore.ChangeNotification> = (change) => {
    let pStr = JSON.stringify(change, null, 2);
    LogUtil.info(pStr);
  }
  
  KvUtil.onDataChange(distributedKVStore.SubscribeType.SUBSCRIBE_TYPE_ALL, callBack);
```

##### offDataChange Unsubscribe to data change notifications

```
KvUtil.offDataChange(callBack);
ToastUtil.showToast('取消订阅数据变更通知');
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

