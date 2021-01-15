//npm模块
const ora = require("ora"); // 输出加载动画
const chalk = require("chalk"); //打印改变颜色
const shell = require("shelljs"); //使用shell
//node模块
const fs = require("fs"); //读取操作文件
const path = require("path"); //读取路径
//常量
const deleteDir = [".git"]; // 需要清理的文件"README.md", ".gitignore"

const modifyConfig = async (answers) => {
  return new Promise((resolve, reject) => {
    const ProjectName = answers.ProjectName;
    answers.name = ProjectName;
    let loading = ora("正在删除多余的git文件，请稍后~");
    loading.start();
    const pwd = shell.pwd();
    deleteDir.map((item) => shell.rm("-rf", pwd + `/${ProjectName}/${item}`));
    if(deleteDir.includes('README.md')){
      //生成一个新的README.md，之前我是想删掉这个文件创建一个新的，后面很多反馈说想看之前的框架写了啥，所以就不删了
      fs.writeFileSync((path.join(__dirname, `./`), `${ProjectName}/README.md`),'');
    }
    loading.succeed(chalk.green("删除成功"));
    loading = ora("正在修改配置文件，请稍后~");
    let jsonData = fs.readFileSync(
      (path.join(__dirname, `./`), `${ProjectName}/package.json`)
    );
    jsonData = JSON.parse(jsonData);
    for (item in answers) {
      jsonData[item] = answers[item];
    }
    const obj = JSON.stringify(jsonData, null, "\t");
    fs.writeFileSync((path.join(__dirname, `./`), `${ProjectName}/package.json`), obj);
    loading.succeed(chalk.green("修改成功"));
    resolve(true);
  });
};

module.exports = modifyConfig;
