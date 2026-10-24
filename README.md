# 学习通自动刷视频 · uXueScript 修改版

基于开源项目 [unraous/uxuescript](https://github.com/unraous/uxuescript) v2.4.1 的 Windows 修改版，
用于超星学习通（i.mooc.chaoxing.com）课程的自动播放与章节任务处理，并修复了 AI 答题的答案解析问题。

> 仅分发修改后的二进制与对应源代码，遵循 GPL-3.0。请自行确认使用场景是否符合所在学校与平台的规定。

## 下载

| 文件 | 说明 |
| --- | --- |
| `dist/uXueScript_2.4.1_quiz-fix4_x64-setup.exe` | Windows x64 安装包（推荐） |
| `dist/uxs-2.4.1-quiz-fix4-win-x64.exe` | 免安装绿色版 |
| `dist/uxuescript-2.4.1-quiz-fix4-source.zip` | 修改版完整源码（GPL-3.0 要求） |

校验值见 `SHA256SUMS.txt`。

## 功能

- 自动播放课程视频，处理文档、PDF 等任务点
- 自动完成章节测验：调用 OpenAI 兼容接口（支持自建中转站）
- 顺序播放、倍速、静音、目录刷新与断点续跑

## 本次修改（相对上游 v2.4.1）

1. 目录同步等待与“课程已完成”判断修复，避免误报完成
2. 旧版 `.ncells` 学习页自动切换到新版入口
3. 测验答案解析兼容
   - 编号列表支持全角句点、顿号、右括号、冒号，同一行内的多个答案可拆分
   - 标题允许加粗或 `#` 前缀；解析段兼容“解析 / 说明 / 分析”；忽略 `---`、`***` 分隔线
   - 模型把 JSON 字符串结尾写成中文引号导致不闭合时，按行补齐后重新解析
4. 任务点出错时保留首个错误并在本轮结束后停止自动重试，不再重复请求同一测验

## 使用

1. 运行安装包，或直接解压绿色版启动
2. 右侧是学习通页面，登录后进入目标课程与章节
3. 左下角配置模型：供应商名称、模型名、请求地址（OpenAI 兼容 `/chat/completions`）、API Key，填好后点 Save
4. 课程区域出现确认提示后点 Yes 开始

配置保存在 `%APPDATA%\top.unraous.uxs\config.toml`，与上游版本共用同一目录。

## 来源与许可

- 上游项目：[unraous/uxuescript](https://github.com/unraous/uxuescript) v2.4.1，作者 unraous
- 许可证：GNU General Public License v3.0，见 [`LICENSE`](LICENSE)
- 本修改版同样以 GPL-3.0 发布，完整源码随 `dist/` 中的 source 包提供
- 修改日期：2026-10-24

## 免责声明

本项目仅供个人学习与技术研究使用。使用本工具产生的一切后果由使用者自行承担，
请遵守学习通平台服务条款及所在院校的学术规范。
