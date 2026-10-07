# Meow Garden 隐私协议

此仓库通过 GitHub Pages 发布已有的多语言隐私协议。

## 在线访问

- 站点首页：https://itozll.github.io/meowdoku-legal/
- 隐私协议入口：https://itozll.github.io/meowdoku-legal/privacy/
- 简体中文：https://itozll.github.io/meowdoku-legal/privacy/zh-Hans.html
- 手动选择语言：https://itozll.github.io/meowdoku-legal/?select=1

两个入口均支持 `?lang=语言代码`，例如 `?lang=zh-Hant`。未指定语言时使用浏览器语言，不支持的语言回退至英语。游戏应将当前选中的语言通过 `lang` 参数传入。

## 发布

GitHub Pages 已配置为从 `privacy` 分支的 `/` 根目录发布。向该分支推送更新后，等待 GitHub Pages 构建完成即可访问。

根目录 `index.html` 提供站点入口；`.nojekyll` 声明直接发布静态文件。所有站内资源使用相对路径，适配 `/meowdoku-legal/` 项目路径。

## 文件与维护

- `privacy/*.md`：隐私协议各语言文本。
- `privacy/*.html`：对应的可访问网页。
- `privacy/style.css`：页面样式。
- `privacy/entry.js`：两个入口共用的语言匹配与跳转逻辑。
- `privacy/index.html`、根目录 `index.html`：语言入口。

支持英语、简体中文、繁体中文、日语、韩语、西班牙语和葡萄牙语。`zh-CN` 文件保留为简体中文兼容地址。

本仓库未包含自动生成脚本。修改协议时须同步对应 Markdown 与 HTML；修改语言入口时须检查两个入口和项目子路径下的链接。
