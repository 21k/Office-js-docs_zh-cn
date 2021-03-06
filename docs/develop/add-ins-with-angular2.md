# <a name="tips-for-creating-office-addins-with-angular-2"></a>使用 Angular 2 创建 Office 外接程序的技巧 

本文提供了使用 Angular 2 将 Office 外接程序创建为单页应用程序的指南。

>**注意：**是否想基于使用 Angular 2 创建 Office 外接程序的体验编写文章？可在 [GitHub](https://github.com/OfficeDev/office-js-docs) 中参与编写这篇文章或通过在存储库中提交 [问题](https://github.com/OfficeDev/office-js-docs/issues) 来提供反馈。 

有关使用 Angular 2 框架构建的 Office 外接程序示例，请参阅 [基于 Angular 2 构建的 Word 样式检查外接程序](https://github.com/OfficeDev/Word-Add-in-Angular2-StyleChecker)。

## <a name="bootstrapping-must-be-inside-officeinitialize"></a>Bootstrapping 必须在 Office.initialize 内

在任意调用 Office、Word 或 Excel JavaScript API 的页面上，代码必须首先向 `Office.initialize` 属性分配一个方法。（如果没有初始化代码，则方法主体可以仅为空的“`{}`”符号，但必须对 `Office.initialize` 属性进行定义。有关详细信息，请参阅 [初始化外接程序](http://dev.office.com/docs/add-ins/develop/understanding-the-javascript-api-for-office#initializing-your-add-in)。）Office 在该方法初始化 Office JavaScript 库后立即对其调用。

**Angular bootstrapping 代码必须在你分配到 `Office.initialize` 的方法内调用**，以确保 Office JavaScript 库首先进行了初始化。以下是演示如何执行该操作的简单示例。此代码应在项目的 main.ts 文件中。

```js
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
    import { AppModule } from './app.module';
    Office.initialize = function () {
        const platform = platformBrowserDynamic();
        platform.bootstrapModule(AppModule);
  };
```

## <a name="use-the-hash-location-strategy-in-the-angular-application"></a>使用 Angular 应用程序中的哈希位置策略

如果不指定哈希位置策略，则在应用程序中的路由间导航可能不起作用。可使用以下两种方法之一完成此操作：首先，可为应用模块中的位置策略指定提供程序，如以下示例中所示。它将进入 app.module.ts 文件。

```js
import { LocationStrategy, HashLocationStrategy } from '@angular/common';
// Other imports suppressed for brevity
    @NgModule({
        providers: [
            {provide: LocationStrategy, useClass: HashLocationStrategy},
            // Other providers suppressed
        ],
        // Other module properties suppressed
  })
  export class AppModule {}
``` 

如果在单独的路由模块中指定路由，则有指定哈希位置策略的替代方法。在路由模块的 .ts 文件中，向指定策略的 `forRoot` 函数传递配置对象。以下代码是一个示例。 

```js
import { RouterModule, Routes } from '@angular/router';
// Other imports suppressed for brevity
    const routes: Routes = // route definitions go here
    @NgModule({
      imports: [ RouterModule.forRoot(routes, {useHash: true}) ],
      exports: [ RouterModule ]
    })
    export class AppRoutingModule {}
```   


## <a name="consider-wrapping-fabric-components-with-angular-2-components"></a>考虑使用 Angular 2 组件打包 Fabric 组件

我们建议在外接程序中使用 [Office UI Fabric](http://dev.office.com/fabric#/fabric-js) 样式。Fabric 包括几个版本的组件，其中包括 [基于 TypeScript](https://github.com/OfficeDev/office-ui-fabric-js) 的版本。考虑通过包装 Angular 2 组件中的 Fabric 组件以在你的外接程序中使用它们。有关演示该步骤的的示例，请参阅 [基于 Angular 2 构建的 Word 样式检查外接程序](https://github.com/OfficeDev/Word-Add-in-Angular2-StyleChecker)。请注意，例如，在 [fabric.textfield.wrapper](https://github.com/OfficeDev/Word-Add-in-Angular2-StyleChecker/blob/master/app/shared/office-fabric-component-wrappers/fabric.textfield.wrapper.component.ts) 中定义的 Angular 组件如何导入定义了 Fabric 组件的 Fabric 文件 TextField.ts。 


## <a name="using-the-office-dialog-api-with-angular"></a>将 Office 对话框 API 与 Angular 结合使用

Office 外接程序对话框 API 可使外接程序打开半模态对话框中的页面，该页面可与主页面交换信息，这在任务窗格中是典型操作。 

[displayDialogAsync](http://dev.office.com/reference/add-ins/shared/officeui.displaydialogasync) 方法采用指定应在对话框中打开的页面的 URL 的参数。外接程序可具有单独的 HTML 页面（与基本页不同）来传递此参数，或在 Angular 应用程序中传递路由的 URL。 

要记住的重要一点是，如果传递路由，则该对话框将创建具有自身执行上下文的新窗口。基本页及其所有初始化和引导代码将在新上下文中再次运行，且任何变量都将被设置为对话框中的初始值。所以，此技术在对话框中启动了单页应用程序的第二个实例。更改了对话框中的变量的代码不会更改同一变量的任务窗格版本。同样，对话框有其自己的会话存储，而任务窗格中的代码不能对其访问。  


## <a name="forcing-an-update-of-the-dom"></a>强制 DOM 的更新

在任意 Angular 2 应用程序中，更新 DOM 的通知偶尔不会触发。框架在 `ApplicationRef` 对象上提供 `tick()` 方法，该方法将强制更新。以下代码是一个示例。

```js
import { ApplicationRef } from '@angular/core';
    export class MyComponent {
        constructor(private appRef: ApplicationRef) {}
        myMethod() {
            // Code that changes the DOM is here
            appRef.tick();
        }
}
``` 

## <a name="using-observables"></a>使用 Observables

Angular 2 使用 RxJS (Reactive Extensions for JavaScript)，而 RxJS 引入了 `Observable` 和 `Observer` 对象以实施异步处理。本部分提供了使用 `Observables` 的简要介绍；有关详细信息，请参阅官方 [RxJS](http://reactivex.io/rxjs/) 文档。

`Observable` 在某种程度上类似一个 `Promise` 对象 - 它立即从异步调用返回，但它可能在以后才能进行解析。不过，`Promise` 是一个值（可以是一个数组对象），而 `Observable` 是对象数组（可能仅有一个成员）。这可使代码调用 `Observable` 对象上的 [数组方法](http://www.w3schools.com/jsref/jsref_obj_array.asp)，如 `concat`、`map` 和 `filter`。 

### <a name="pushing-instead-of-pulling"></a>使用“推送”代替“拉取”

代码“拉取” `Promise` 对象（通过将其分配到变量），而 `Observable` 对象将其值“推送”到*订阅* `Observable` 的对象。订阅服务器是 `Observer` 对象。推送体系结构的优势是，随着时间的推移，新成员可以添加到 `Observable` 数组。添加了新成员后，订阅 `Observable` 的所有 `Observer` 对象都将收到一条通知。 

`Observer` 被配置为使用一个函数处理每个新对象（称为“next”对象）。（它还被配置为响应一个错误和一个完成通知。参阅下一部分的一个示例。）为此，与 `Promise` 对象相比，`Observable` 对象的使用范围更广。例如，除了从 AJAX 调用返回 `Observable`（即返回 `Promise` 的方式）以外，还可从事件处理程序返回 `Observable`，例如文本框的“已更改”事件处理程序。用户每次在框中输入文本时，所有已订阅的 `Observer` 对象将使用最新文本和/或输入的应用程序的当前状态立即做出反应。 


### <a name="waiting-until-all-asynchronous-calls-have-completed"></a>等待所有异步调用完成

如果想要确保仅当一组 `Promise` 对象的每个成员解析后运行撤消，请使用 `Promise.all()` 方法。

```js
myPromise.all([x, y, z]).then(// TODO: Callback logic goes here.)
``` 

若要使用 `Observable` 对象执行同一操作，请使用 [Observable.forkJoin()](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/operators/forkjoin.md) 方法。  

```js
var source = Rx.Observable.forkJoin([x, y, z]);

var subscription = source.subscribe(
  function (x) {
    // TODO: Callback logic goes here
  },
  function (err) {
    console.log('Error: ' + err);
  },
  function () {
    console.log('Completed');
  });
``` 

