//npm模块
const shell = require('shelljs');//使用shell
const chalk = require('chalk');//打印改变颜色
//node模块
const fs =require('fs');//读取操作文件
//本地文件的引入
const clone = require('./clone');//获取模板
const questions = require('./questions');//用户选择模板
const modifyConfig = require('./modify-config');//修改配置
const install = require('./install');//安装依赖


const initAction = async(name) => {
    let ProjectName = ""
    //获取项目名称
    if(typeof(name.init) === "string"){
        ProjectName = name.init
    }
    //先判断下git能不能用，不能用就不用白忙活了
    if(!shell.which('git')){
        console.log(chalk.red('找不到git,请先检查git是否可用'));
        return 
    }
    if(ProjectName){
        if(fs.existsSync(ProjectName) || ProjectName.match(/[^A-Za-z0-9\u4e00-\u9fa5_-]/g)){
            ProjectName = ""
        }
    }
    //获取用户输入的结果
    const answers = await questions(ProjectName);
    const starttime = new Date().getTime()
    if(answers.ProjectName){
        ProjectName = answers.ProjectName
    }
    //下载模板
    const CloneFind = await clone(ProjectName,answers.url)
    if(!CloneFind){
        return
    }
    //修改配置文件
    await modifyConfig({...answers,ProjectName:ProjectName})
    //看看要不要安装npm依赖
    if(answers.need !== "否"){
        await install(ProjectName,answers.need)
    }
    console.log(chalk.green(`项目构建成功,耗时${(new Date().getTime() - starttime)/1000}s，cd ${ProjectName} 开始开发吧，加油哦！`));
}

module.exports = initAction