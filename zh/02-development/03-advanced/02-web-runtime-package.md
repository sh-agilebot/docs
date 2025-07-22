---
url: /zh/02-development/03-advanced/02-web-runtime-package.md
---
# Web小程序的运行库

我们提供了Web小程序的运行库，可以方便的调用一些方法。

您可以通过包管理工具来安装：

::: code-group

```sh [npm]
npm install @agilebot/extension-runtime
```

```sh [yarn]
yarn add @agilebot/extension-runtime
```

```sh [pnpm]
pnpm add @agilebot/extension-runtime
```

:::

也可以直接在浏览器中引用：

```html
<script src="https://unpkg.com/@agilebot/extension-runtime/dist/browser.js"></script>
```

当您使用 `<script>` 标签在浏览器中直接引入运行库时，所有的导出方法会挂载在全局命名空间 `gbtExtension` 上。

例如，如果您需要获取当前语言，不需要使用 import，而是可以直接调用：

```html
<script>
  gbtExtension.getLanguage().then(function (lang) {
    console.log(`当前语言为：${lang}`);
  });
</script>
```

## 多语言

当Web小程序在AgileLink中打开时，需要获取App当前的语言，进而切换用户Web小程序的语言与App一致。可以采用下面的方式实现该功能。

示例代码：

```ts twoslash
import { getLanguage } from '@agilebot/extension-runtime';

const currentLang = await getLanguage();
console.log(`当前的语言: ${currentLang}`);
```

## 启用快捷按键 {#enable-shortcut}

当插件的Web页打开时，一些快捷按键将被禁用，如工业示教器上的物理按钮。您可以通过以下方式启用快捷按键：

```ts twoslash
import { enableShortcut } from '@agilebot/extension-runtime';

enableShortcut();
```

:::danger 危险
如不调用此方法，可能导致的后果：

* 工业示教器锁屏后，屏幕将无法通过物理按钮来唤醒
* 只能通过长按示教器电源按钮15秒以上，进行强制关机并重启
  :::

## 显示弹框等组件

为了与AgileLink保持一致的风格，我们提供了一些常用函数用于展示通知消息和弹框。

```ts twoslash
import { rtmNotification, rtmMessageBox } from '@agilebot/extension-runtime';

// 显示信息通知
rtmNotification.info('这是一个信息消息');
// 显示错误通知
rtmNotification.error('这是一个错误消息');
// 显示成功通知
rtmNotification.success('操作成功');
// 显示警告通知
rtmNotification.warning('这是一个警告消息');

// 显示确认对话框
rtmMessageBox
  .confirm('您确定要删除吗？')
  .then(() => {
    console.log('用户确认了操作');
  })
  .catch(() => {
    console.log('用户取消了操作');
  });
```

## 获取插件的状态

您可以通过以下方式获取某个插件的当前状态：

```ts twoslash
import { getExtensionState } from '@agilebot/extension-runtime';

const extension = await getExtensionState('myService');
console.log(
  `插件是否已经启用: ${extension.enabled}, 端口号：${extension.port}`
);
```

## 是否处于插件环境中

本地调试Web页面时，可以判断当前运行在插件环境还是本地电脑：

```ts twoslash
import { isInExtension } from '@agilebot/extension-runtime';

console.log(`当前是否处于插件环境：${isInExtension()}`);
```
