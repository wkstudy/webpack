## 记录
从make阶段开始

`grep -nr hooks.make ./lib` 找到`EntryPlugin.js`的调用
```
<!-- 入口文件 被初始化为一个class EntryDependency -->
// EntryPlugin.js
compilation.addEntry()
```
compilation  addEntry 共做了两件事
```
1. 入口文件存到 dependencies中
2. addModuleTree()
  2.1 handleModuleCreation()
```

```
handleModuleCreation () {

  	const moduleGraph = this.moduleGraph;
    const currentProfile = this.profile ? new ModuleProfile() : undefined;
    this.factorizeModule(
			{
				currentProfile,
				factory,
				dependencies,
				factoryResult: true,
				originModule,
				contextInfo,
				context
			},)
}
```
没找到addentry之后是从哪里开始resolve module的



从compilation的build方法开始
_buildModule()  =>module.build()

_build里  runloader()  => 其他格式文件=》js代码， 并分析出相关依赖
