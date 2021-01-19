//npm模块
const ora = require("ora"); // 输出加载动画
const chalk = require("chalk"); //打印改变颜色
const shell = require("shelljs"); //使用shell

const install = (ProjectName,Way) =>{
    return new Promise(async (resolve, reject) => {
        const loading = ora('依赖安装中，请稍后~');
        loading.start()
        shell.cd(ProjectName)
        if (shell.exec(Way).code !== 0) {
            console.log(chalk.yellow('自动安装失败，请手动安装！'));
            loading.fail(); // 安装失败
            shell.exit(1);
        }
        loading.succeed(chalk.green('依赖安装成功！'));
        resolve()
    })
}

module.exports = install