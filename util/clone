//npm模块
const download = require("download-git-repo"); //下载利器
const ora = require("ora"); // 输出加载动画
const chalk = require("chalk"); //打印改变颜色

const clone = async (name, url) => {
  return new Promise((resolve, reject) => {
    console.log(chalk.blue('远程下载地址:'+url));
    const loading = ora("正在从git上下载模板，请稍后~");
    loading.start();
    download(url, name, { clone: true }, (err) => {
      if (err) {
        loading.fail();
        console.log(chalk.red("下载模板错误:" + err));
        resolve(false);
        return;
      }
      loading.succeed(chalk.green("下载模板成功"));
      resolve(true);
    });
  });
};

module.exports = clone;
