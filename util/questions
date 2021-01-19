//npm模块
const inquirer = require("inquirer"); //交互问答机
//本地文件
const defaultUrl = require("./default-url"); //获取配置的模板地址
//常量
const installWay = [
  { key: "a", name: "npm install", value: "npm install" },
  { key: "b", name: "cnpm install", value: "cnpm install" },
  { key: "c", name: "yarn install", value: "yarn install" },
  { key: "d", name: "否", value: "否" },
];

const questions = (ProjectName) => {
  return new Promise(async (resolve, reject) => {
    const urlList = await defaultUrl();
    const rule = [
      {
        type: "input",
        message: "请输入项目名称:",
        name: "ProjectName",
        when() {
          return !ProjectName;
        },
        validate(val) {
          if (!val) {
            return "模板名称不能为空！";
          } else if (!val.match(/^[a-z]+$/g)) {
            return "模板名称只能是小写字母组成，请重新输入";
          }
          return true;
        },
      },
      { type: "input", message: "请输入项目简介:", name: "description" },
      { type: "input", message: "请输入作者名字:", name: "author" },
      {
        type: "list",
        message: "是否采用系统模板:",
        name: "way",
        choices: ["是", "否"],
      },
      {
        type: "input",
        message: "请输入要clone的项目地址:",
        name: "url",
        when(answers) {
          // 当way选择为否的时候才会提问当前问题
          return answers.way === "否";
        },
        validate(val) {
          if (!val) {
            return "项目地址不能为空！";
          } else if (val.match(/^(?!direct:http).*/g)) {
            return "项目地址不符合，请重新输入";
          }
          return true;
        },
        filter(val) {
          return "direct:" + val;
        },
      },
      {
        type: "list",
        message: "请选择模板类型:",
        name: "url",
        choices: urlList,
        when(answers) {
          // 当way选择为是的时候才会提问当前问题
          return answers.way === "是";
        },
      },
      {
        type: "list",
        message: "是否需要自动安装依赖:",
        name: "need",
        choices: installWay,
      },
    ];
    const answers = await inquirer.prompt(rule);
    resolve(answers);
  });
};

module.exports = questions;
