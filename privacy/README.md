# 隐私协议维护与 GitHub Pages 发布

## 支持的语言

协议使用与游戏 `I18n.ts` 一致的七种语言代码。每种语言都有完整的十节协议和对应 HTML 网页。

| 游戏语言代码 | 语言 | 协议源码 | 网页 |
| --- | --- | --- | --- |
| en | English | en.md | en.html |
| zh-Hans | 简体中文 | zh-Hans.md | zh-Hans.html |
| zh-Hant | 繁體中文 | zh-Hant.md | zh-Hant.html |
| ja | 日本語 | ja.md | ja.html |
| ko | 한국어 | ko.md | ko.html |
| es | Español | es.md | es.html |
| pt | Português | pt.md | pt.html |

开发者 gaoguodong，联系邮箱 joiky@163.com，更新及生效日期 2026-10-07。旧的 `zh-CN.md` 和 `zh-CN.html` 保留为简体中文兼容文件，由生成脚本同步。

## 通用入口与游戏语言

站点根目录 `/` 和 `/privacy/` 均为通用入口，自动跳转至对应语言的协议：

1. 优先使用 URL 中非空的 `lang` 参数。游戏或宿主打开协议时应将当前选中的 `i18n.locale` 传给此参数，避免游戏语言和设备语言不同。
2. 未指定 `lang` 时，按浏览器 `navigator.languages` 的顺序匹配第一个支持的语言；没有该列表时使用 `navigator.language`。
3. 未支持的语言回退至英语。显式传入未支持的 `lang` 也回退至英语。

示例通用 URL：`https://itozll.github.io/meowdoku-cocos/privacy/?lang=zh-Hant`。传入 `ja`、`ko`、`es` 或 `pt` 可进入对应页面；`pt-BR` 与 `pt-PT` 均匹配 `pt`，`es-MX` 匹配 `es`。中文优先按显式的 Hans/Hant 脚本匹配；没有脚本时，TW/HK/MO 使用繁体，其他中文使用简体。也兼容大小写及下划线分隔的语言代码。

浏览器无法自动读取另一个域名或宿主内的游戏语言设置。因此游戏选择的语言需通过 `lang` 明确传入，不能仅依赖浏览器语言。此任务提供网页入口及参数，不向游戏增加新的按钮。

添加 `?select=1` 可停留在手动选择页。协议页顶部也有七语言选择菜单；禁用 JavaScript 时仍可通过通用入口的七个链接选择语言。直接访问各语言 `.html` 文件不会被浏览器语言覆盖。

`entry.js` 只在浏览器内读取 URL 与浏览器语言，不读取或写入本地存储，不设置 Cookie，也不发起第三方请求。URL 目标仅从七种受支持的语言中选择，不允许任意外部跳转。根目录和 `/privacy/` 入口都支持 GitHub Pages 项目子路径。

## 修改与生成

- `style.css`：本站样式，不引用第三方字体或图片。
- `entry.js`：自动入口，仅入口页加载，协议正文页不加载脚本。
- `index.html` / `../index.html`：协议目录及站点根目录的通用入口。
- `../../scripts/build-privacy-pages.py`：使用 Python 标准库从 Markdown 生成网页。

修改七种规范语言的 `.md` 源码后，在仓库根目录运行 `python scripts/build-privacy-pages.py`，同时提交源码和生成网页。不要直接编辑生成的 `.html` 或兼容文件 `zh-CN.md`。

## 内容依据

源模板为 `docs/用户隐私保护指引设置.docx`。模板的注册登录、昵称、手机号、身份证、固定中国大陆存储地点及不存在的授权撤回路径未直接沿用。

实现依据为 `Progress.ts`、`Puzzle.ts`、`i18n/I18n.ts`、`MeowGarden.ts`、`AdsService.ts` 和 `PlatformConfig.ts`：当前无账号、云存档和支付；本地存储键为 `meow-garden.v1` 与 `meow-garden.language`；广告创建仅传入广告位 ID，奖励由完成回调判断。协议区分宿主独立处理与游戏代码直接处理。

在实际海外宿主接入与上线时仍需核对宿主名称及政策、实际广告供给方、SDK 版本、数据类别、保存地点与期限、跨境保障、广告同意和儿童相关配置。修改平台或处理行为时应同步更新全部语言，不能把本协议当作 SDK 数据行为或平台合规的验证结果。

参考官方入口：

- [SUD 隐私政策入口](https://www.sud.tech/privacy)
- [GitHub Pages 数据收集](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages#data-collection)
- [GitHub 隐私声明](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement)
- [GitHub Pages 发布源设置](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

## 专用分支发布

本协议专用分支为 `codex/privacy-policy`。协议提交到此分支，不要求先合并到 `main`。

由仓库管理员在 Settings → Pages 设置：

1. Source 选择 Deploy from a branch。
2. Branch 选择 `codex/privacy-policy`，目录选择 `/docs`，保存。
3. 等待 Pages 构建成功，确认公开页面可访问。

私有仓库需要支持私有仓库 Pages 的 GitHub 付费方案；普通分支推送权限不足以更改 Pages 设置。本项目没有为发布改变仓库可见性。Pages 发布会暴露 `/docs` 下的静态文件，管理员启用前应确认这些文件可公开。

预期通用入口为 `https://itozll.github.io/meowdoku-cocos/`，以及 `https://itozll.github.io/meowdoku-cocos/privacy/`。以实际 Pages 返回的 URL 为准，不能据此判断已上线。后续在此分支推送协议更新将触发 Pages 发布，不要删除作为发布源的专用分支。

## 验证与发布状态

2026-10-07：Chrome 无头浏览器验证七种协议页面，覆盖 390×844 手机与 1280×844 桌面视口；十节内容、开发者与邮箱、语言菜单、切换和本地链接均正常，无横向溢出。验证两个入口共 28 次显式语言跳转，五种浏览器地区语言匹配，旧 `zh-CN.html` 链接兼容，以及禁用 JavaScript 时的手动选择。页面未发起外部资源请求。

入口的六组定向测试全部通过，覆盖显式语言优先、繁简及地区语言、浏览器语言顺序、英语回退、空值、非法参数和手动入口。执行命令为 `node --test tests/privacy-entry.test.cjs`。`git diff --check` 通过。本次未修改游戏代码，未运行游戏全量测试。

首次发布时当前 GitHub 身份具有 push 权限，但 admin、maintain 均为 false；尝试创建 Pages 站点时 API 返回 HTTP 404，本次未能启用 Pages。需要仓库管理员按上方步骤设置发布源，之后再确认实际发布 URL 与构建结果。
