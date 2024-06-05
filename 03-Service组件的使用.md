# Service组件的使用

## 1.Service组件的概述

Service组件是Android四大组件之一，它主要用于在后台执行耗时任务，并且没有界面。

Service组件的两种使用方式：

- 启动方式：startService
- 绑定方式：bindService

## 2.Service组件的启动方式

### 2.1 创建Service组件的配置文件

```xml
<service
    android:name=".MyService"
    android:enabled="true"
    android:exported="true">
</service>
```

### 2.2 创建Service组件

```java
public class MyService extends Service {
    private static final String TAG = "MyService";

    private MyBinder mBinder = new MyBinder();

    @Override
    public IBinder onBind(Intent intent) {
        return mBinder;
    }

    @Override
    public void onCreate() {
        super.onCreate();
        Log.d(TAG, "onCreate: ");
    }

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        Log.d(TAG, "onStartCommand: ");
        return super.onStartCommand(intent, flags, startId);
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
        Log.d(TAG, "onDestroy: ");
    }

	// 一个子类Binder
    public class MyBinder extends Binder {
        public void startDownload() {
            Log.d(TAG, "startDownload: ");
        }
        public void stopDownload() {
            Log.d(TAG, "stopDownload: ");
        }
    }
}
```

### 2.3 绑定Service组件

```java
Intent intent = new Intent(this, MyService.class);
bindService(intent, mConnection, BIND_AUTO_CREATE);
```

### 2.4 解绑Service组件

```java
unbindService(mConnection);
```

### 2.5 启动Service组件

在Activity中使用startService方法来启动Service组件，调用startService方法后，Service组件会立即执行onCreate方法，然后执行onStartCommand方法。

```java
Intent intent = new Intent(this, MyService.class);
startService(intent);
```

### 2.6 停止Service组件

在Activity中使用stopService方法来停止Service组件，调用stopService方法后，Service组件会立即执行onDestroy方法。

```java
Intent intent = new Intent(this, MyService.class);
stopService(intent);
```

### 2.7 启动Service组件的注意事项

- 启动Service组件后，Service组件会立即执行onCreate方法，然后执行onStartCommand方法。
- 启动Service组件后，Service组件会一直运行，直到调用stopService方法或者Service组件被系统回收。
- 启动Service组件后，Service组件会一直运行，直到调用stopService方法或者Service组件被系统回收。
- 启动Service组件后，Service组件会一直运行，直到调用stopService方法或者Service组件被系统回收。