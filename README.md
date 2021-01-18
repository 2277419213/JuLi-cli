# juli-cli快速搭建项目脚手架   

因为平时有自己开源的项目框架，包括一些移动端自适应，或者pc端整合了模板啥的框架，为了方便团队快速下载复用构建，于是自己搭建了一个脚手架。

```
//全局安装
npm install -g juli-cli 

//查看版本
juli-cli -V

//初始化框架
juli-cli -I [name] 或者 juli-cli --init [name]
```

### 配置模板   

模板参数说明
| 键 | 值 |
| :--- | :--- |
| key | 索引，要保持唯一 |
| name | 模板的名称 |
| value | 模板对应的地址，http前面要带direct: |

模板相关命令说明
| 命令 | 说明 |
| :--- | :--- |
| npm config set juliurl urlList | 设置模板地址，重复设置可以覆盖 |
| npm config get juliurl | 查看设置的模板地址，若为undefined，则未设置 |
| npm config delete juliurl | 删除所设置的模板 |
      
示例   
```js
    //写一个模板数组
    let urlList = [{
      key: "a",
      name: "居里移动端自适应框架",
      value: "direct:https://github.com/2277419213/vue_h5_dome",
    },
    {
      key: "b",
      name: "花裤衩后台管理框架",
      value:
        "direct:https://github.com/PanJiaChen/vue-admin-template#/permission-control",
    }]
    //JSON.stringify格式化一下,这里你有很多种方法可以去操作，甚至在谷歌浏览器F12里面操作也是可行的
    urlList = JSON.stringify(urlList)
    //这是JSON.stringify后的结果，甚至你直接复制我这个改也可以："[{"key":"a","name":"居里移动端自适应框架","value":"direct:https://github.com/2277419213/vue_h5_dome"},{"key":"b","name":"花裤衩后台管理框架","value":"direct:https://github.com/PanJiaChen/vue-admin-template#/permission-control"}]"
    
    //然后打开终端，确保在有npm的前提下，输入npm config set juliurl <urlList>
    //注意这里名字一定要是juliurl
    ```
    npm config set juliurl "[{"key":"a","name":"居里移动端自适应框架","value":"direct:https://github.com/2277419213/vue_h5_dome"},{"key":"b","name":"花裤衩后台管理框架","value":"direct:https://github.com/PanJiaChen/vue-admin-template#/permission-control"}]"
    ```
    //这样模板就配置好了
```



### 版本说明

- 1.0.0   
完成功能开发，提交初代版本。

- 1.0.1   
修改一个错别字，关联github仓库

- 1.0.2   
新增配置自己项目长用的模板，一次配置，永久便携使用，更适合小团队和公司

