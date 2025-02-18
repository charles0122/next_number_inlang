## Inlang 项目

用于nextnumber的多语言重构
配合easy_localization

### 注意点
默认选择了en语言作为inlang的引用语言
除非你了解该文件夹内的工作原理，不然不要轻易去移动或修改除（translations文件夹）以外的其他目录

### 多语言工作流程

1. （规范性）将页面或domain下需要进行多语言的文本提取为一个map，并将map存到en.json文件（该文件在该项目中被inlang引用）

eg：
store文件下以下文本需要多语言处理

```dart

var widgets = [
Text("Select number"),
Text("无更多数据"),
Text("加载失败，请稍后重试"),
];

```
(规范性)：key 使用小驼峰命名法
```json
{
    "store":{
      "selectNumber": "Select number",
      "noMoreData": "No more data",
      "loadFailed": "Load failed, Please try again!"
    }
}
```

2. （可选）使用机器翻译生成其他的语言文本，然后生成代码中可使用的 LocaleKeys.dart 文件
如果你使用bun，可以使用以下命令

```shell
# 需先执行 bun install 按照所需要的依赖。
bun inlang machine translate --project ./project.inlang
# 更多信息 https://inlang.com/m/2qj2w8pu/app-inlang-cli
```

```shell
fvm flutter pub run easy_localization:generate -S inlang/translations -f keys -O lib/core/generated -o locale_keys.g.dart
# 更多信息 https://pub.dev/packages/easy_localization
```

3. 推送到仓库 next_number_inlang

4. （专业翻译或运营）使用fink 进行翻译，翻译完成后推送即可
链接 https://fink.inlang.com/github.com/charles0122/next_number_inlang?project=%2Fproject.inlang&lang=en&lang=ar&lang=bn&lang=es&lang=fr&lang=hi&lang=id&lang=pt&lang=th&lang=vi&lang=zh-CN

5. （开发）拉取更新后的翻译仓库

### 新增语言步骤
1 在translations目录下新增一个符合文件命名标准的json文件 (它需要是有效的 BCP-47 语言标签)
比如 zh-Hans.json

2 （可选）运行机器翻译
