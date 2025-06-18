<p align="center">
  <a href="https://github.com/ispace-top/waka-readme-stats">
    <img src="https://user-images.githubusercontent.com/25841814/79395484-5081ae80-7fac-11ea-9e27-ac91472e31dd.png" alt="Project Preview" width="400"/>
  </a>
</p>

<h3 align="center">📌✨ 你的 GitHub Readme 开发统计数据（定制版）</h3>

<p align="center">
  这个项目是 <a href="https://github.com/anmol098/waka-readme-stats">anmol098/waka-readme-stats</a> 的一个定制分支，它能帮助你在 GitHub 个人资料 README 中展示你的开发活动统计数据。
</p>

---

<p align="center">
   <img src="https://img.shields.io/badge/language-python-blue?style"/> 
   <img src="https://img.shields.io/github/license/ispace-top/waka-readme-stats"/> 
   <img src="https://img.shields.io/github/stars/ispace-top/waka-readme-stats"/> 
   <img src="https://img.shields.io/github/forks/ispace-top/waka-readme-stats"/> 
   <img src="https://img.shields.io/static/v1?label=%F0%9F%8C%9F&message=如果%20有用&style=flat&color=BC4E99" alt="Star Badge"/>
</p>
<p align="center">
   你是早起的鸟儿 🐤 还是夜猫子 🦉？
   <br/>
   你一天中什么时候效率最高？
   <br/>
   你主要使用什么编程语言？
   <br/>
   让我们在你的个人资料中展示这些数据！
</p>

<p align="center">
    <a href="https://github.com/ispace-top/waka-readme-stats/issues/new?assignees=anmol098&labels=bug&template=bug_report.md&title=BUG">报告 Bug</a>
    ·
    <a href="https://github.com/ispace-top/waka-readme-stats/issues/new?assignees=anmol098&labels=Brainstorming&template=feature_request.md&title=FEAT">请求新功能</a>
</p>

## ✨ 定制修改内容

此定制版在原版基础上进行了以下改进：

1.  修复了第一行标题可能出现的 UI 渲染异常问题。
2.  新增 `README_FILE` 字段，用于控制更新的 README 文件名称，支持多语言文件更新。

## 🚀 使用示例

为了更新你的 README 文件，你可以在 GitHub Actions 中配置以下工作流：

```yml
name: Waka Readme

on:
  schedule:
    # 每天 IST 12am 运行
    - cron: '30 18 * * *'
  workflow_dispatch:
jobs:
  update-readme:
    name: Update Readme with Metrics
    runs-on: ubuntu-latest
    steps:
      # Checkout 仓库，以便操作文件
      - uses: actions/checkout@v3
      - name: Update Chinese Readme
        uses: docker://wapedkj/waka-readme-stats:master
        with:
          WAKATIME_API_KEY: ${{ secrets.WAKATIME_API_KEY }}
          GH_TOKEN: ${{ secrets.GH_TOKEN }}
          LOCALE: zh
          README_FILE: README.md # 指定更新中文 README
          SHOW_SHORT_INFO: False
          SHOW_TIMEZONE: False
          SHOW_OS: False
          SHOW_LANGUAGE: False
          SHOW_EDITORS: False
          SHOW_PROJECTS: False
          SHOW_LINES_OF_CODE: False
          SHOW_TOTAL_CODE_TIME: False
          SHOW_PROFILE_VIEWS: false
          SHOW_DAYS_OF_WEEK: false
      - name: Update English Readme
        uses: docker://wapedkj/waka-readme-stats:master
        with:
          WAKATIME_API_KEY: ${{ secrets.WAKATIME_API_KEY }}
          GH_TOKEN: ${{ secrets.GH_TOKEN }}
          LOCALE: en
          README_FILE: README_en.md # 指定更新英文 README
          SHOW_SHORT_INFO: False
          SHOW_TIMEZONE: False
          SHOW_OS: False
          SHOW_LANGUAGE: False
          SHOW_EDITORS: False
          SHOW_PROJECTS: False
          SHOW_LINES_OF_CODE: False
          SHOW_TOTAL_CODE_TIME: False
          SHOW_PROFILE_VIEWS: false
          SHOW_DAYS_OF_WEEK: false
```

## ⚙️ 准备工作

1.  **更新你的 README**: 在你的 `README.md` 文件中添加以下注释。这些行将作为我们注入开发统计数据的入口点。

    ```md
    <!--START_SECTION:waka-->
    <!--END_SECTION:waka-->
    ```

2.  **获取 WakaTime API Key**: 你可以在 WakaTime 的账户设置中获取你的 API Key。如果你是 WakaTime 新用户，请访问 [https://wakatime.com](https://wakatime.com) 创建账户并安装 [WakaTime 插件](https://wakatime.com/plugins) 到你喜欢的编辑器/IDE。

3.  **获取 GitHub API Token**: 为了获取提交指标，你需要一个具有 `repo` 和 `user` 范围的 GitHub 访问令牌。你可以在 [这里](https://github.com/settings/tokens) 找到它。
    > **注意**: 启用 `repo` 范围看起来**很危险**，但此 GitHub Action 只会访问你的提交日期、时间以及你在所贡献仓库中添加或删除的代码行数。

4.  **保存 API Key 和 Token**: 将你的 WakaTime API Key 和 GitHub API Token 作为仓库的 Secrets。在你的仓库设置中，保存它们，例如：
    * WakaTime API Key 为 `WAKATIME_API_KEY=<你的 WakaTime API Key>`
    * GitHub 个人访问令牌为 `GH_TOKEN=<你的 GitHub 访问令牌>`

5.  **启用/禁用 Feature Flags**: 你可以根据自己的需求启用或禁用各种功能标志（见下方“可用 Flag”部分）。

此 Action 将在每天 IST 00:00 运行。

## ➕ 可用 Flag

以下是可以在工作流文件中配置的额外 `FLAG`，以自定义你的统计数据显示。默认情况下，除了 `SHOW_LINES_OF_CODE` 之外，所有 Flag 都已启用。

-   `LOCALE`: 用于显示你选择语言的统计数据。默认是英语，使用 [Locale 缩写形式](https://saimana.com/list-of-country-locale-code/) 来设置。
-   `SHOW_LINES_OF_CODE`: 设置为 `True` 将显示你截至目前编写的总代码行数。
    ![Lines of Code](https://img.shields.io/badge/%E4%BB%8E%20Hello%20World%20%E6%88%91%E5%B7%B2%E7%BB%8F%E5%86%99%E4%BA%86-1.3%20%E7%99%BE%E4%B8%87%20%E8%A1%8C%E4%BB%A3%E7%A0%81-blue)
-   `SHOW_PROFILE_VIEWS`: 设置为 `False` 将隐藏你的个人资料浏览量。
    ![Profile Views](http://img.shields.io/badge/%E4%B8%AA%E4%BA%BA%E8%B5%84%E6%96%99%E8%A7%82%E7%9C%8B%E6%AC%A1%E6%95%B0-2189-blue)
-   `SHOW_COMMIT`: 设置为 `False` 将隐藏提交统计图表。
    **我是早起的 🐤**
    ```text
    🌞 早晨    95 commits     ███████░░░░░░░░░░░░░░░░░░   30.55%
    🌆 白天    78 commits     ██████░░░░░░░░░░░░░░░░░░░   25.08%
    🌃 傍晚    112 commits    █████████░░░░░░░░░░░░░░░░   36.01%
    🌙 晚上      26 commits     ██░░░░░░░░░░░░░░░░░░░░░░░   8.36%
    ```
-   `SHOW_DAYS_OF_WEEK`: 设置为 `False` 将隐藏每周不同天的提交统计。
    📅 **我最有效率是在星期日**
    ```text
    星期一       50 commits     ███░░░░░░░░░░░░░░░░░░░░░░   13.19%
    星期二      85 commits     █████░░░░░░░░░░░░░░░░░░░░   22.43%
    星期三    56 commits     ███░░░░░░░░░░░░░░░░░░░░░░   14.78%
    星期四     44 commits     ███░░░░░░░░░░░░░░░░░░░░░░   11.61%
    星期五       28 commits     █░░░░░░░░░░░░░░░░░░░░░░░░   7.39%
    星期六     30 commits     ██░░░░░░░░░░░░░░░░░░░░░░░   7.92%
    星期日       86 commits     █████░░░░░░░░░░░░░░░░░░░░   22.69%
    ```
-   `SHOW_LANGUAGE`: 设置为 `False` 将隐藏你使用的编程语言列表。
    ```text
    💬 编程语言:
    JavaScript               5 hrs 26 mins       ███████████████░░░░░░░░░░   61.97%
    PHP                      1 hr 35 mins        ████░░░░░░░░░░░░░░░░░░░░░   18.07%
    Markdown                 1 hr 9 mins         ███░░░░░░░░░░░░░░░░░░░░░░   13.3%
    Python                   22 mins             █░░░░░░░░░░░░░░░░░░░░░░░░   4.32%
    XML                      8 mins              ░░░░░░░░░░░░░░░░░░░░░░░░░   1.62%
    ```
-   `SHOW_OS`: 设置为 `False` 将隐藏操作系统使用情况。
    ```text
    💻 操作系统:
    Windows                  8 hrs 46 mins       █████████████████████████   100.0%
    ```
-   `SHOW_PROJECTS`: 设置为 `False` 将隐藏你工作过的项目列表。
    ```text
    🐱‍💻 项目:
    ctx_connector            4 hrs 3 mins        ███████████░░░░░░░░░░░░░░   46.33%
    NetSuite-Connector       1 hr 31 mins        ████░░░░░░░░░░░░░░░░░░░░░   17.29%
    mango-web-master         1 hr 12 mins        ███░░░░░░░░░░░░░░░░░░░░░░   13.77%
    cable                    54 mins             ██░░░░░░░░░░░░░░░░░░░░░░░   10.41%
    denAPI                   40 mins             ██░░░░░░░░░░░░░░░░░░░░░░░   7.66%
    ```
-   `SHOW_TIMEZONE`: 设置为 `False` 将隐藏你的时区。
    ```text
    ⌚︎ 时区: America/Sao_Paulo
    ```
-   `SHOW_EDITORS`: 设置为 `False` 将隐藏你使用的代码编辑器。
    ```text
    🔥 编辑器:
    WebStorm                 6 hrs 47 mins       ███████████████████░░░░░░   77.43%
    PhpStorm                 1 hr 35 mins        ████░░░░░░░░░░░░░░░░░░░░░   18.07%
    PyCharm                  23 mins             █░░░░░░░░░░░░░░░░░░░░░░░░   4.49%
    ```
-   `SHOW_LANGUAGE_PER_REPO`: 设置为 `False` 将隐藏不同仓库中使用的语言或框架数量。
    **我最常使用 Vue**
    ```text
    Vue          8 repos        ██████░░░░░░░░░░░░░░░░░░░   25.0%
    Java         6 repos        ████░░░░░░░░░░░░░░░░░░░░░   18.75%
    JavaScript   6 repos        ████░░░░░░░░░░░░░░░░░░░░░   18.75%
    PHP          3 repos        ██░░░░░░░░░░░░░░░░░░░░░░░   9.38%
    Python       2 repos        █░░░░░░░░░░░░░░░░░░░░░░░░   6.25%
    Dart         2 repos        █░░░░░░░░░░░░░░░░░░░░░░░░   6.25%
    CSS          2 repos        █░░░░░░░░░░░░░░░░░░░░░░░░   6.25%
    ```
-   `SHOW_SHORT_INFO`: 设置为 `False` 将隐藏关于用户的简短信息。
    > 此部分需要具有用户权限的个人访问令牌，否则显示的数据可能不正确。
    **🐱 我的 GitHub 数据**
    > 🏆 2020 年贡献 433 次
    > 📦 在 GitHub 存储中使用了 292.3 kB
    > 💼 开放招聘
    > 📜 25 个公共仓库
    > 🔑 15 个私人仓库
-   `SHOW_LOC_CHART`: 设置为 `False` 将隐藏每年不同季度编写的代码行数图表。
    **时间线**
    ![Chart Not Found](https://raw.githubusercontent.com/anmol098/anmol098/master/charts/bar_graph.png)
-   `SHOW_UPDATED_DATE`: 设置为 `False` 将隐藏上次更新日期。
-   `SHOW_TOTAL_CODE_TIME`: 设置为 `False` 将隐藏总编码时间。
-   `COMMIT_BY_ME`: 设置为 `True` 将使用你自己的姓名和电子邮件进行 Git 提交。
-   `COMMIT_MESSAGE`: 自定义 Git 提交消息。
-   `COMMIT_USERNAME`: 自定义 Git 提交用户名。
-   `COMMIT_EMAIL`: 自定义 Git 提交电子邮件。
-   `COMMIT_SINGLE`: 设置为 `True` 将在每次提交时擦除提交历史。
-   `UPDATED_DATE_FORMAT`: 更新日期的格式。
-   `IGNORED_REPOS`: 不希望被统计的仓库列表，用逗号分隔。
-   `SYMBOL_VERSION`: 进度条的符号版本，可选 `1`、`2`、`3`。
-   `DEBUG_LOGGING`: 是否启用 Action 调试日志。
-   `DEBUG_RUN`: 是否以调试模式运行。

## ❤️ 支持项目

如果你觉得这个项目有用，可以通过以下方式支持我：

* 在使用此 Action 时在你的 README 中注明，并链接回此仓库。
* 给项目一个 Star ⭐ 并分享。

感谢！

## 鸣谢

* [anmol098/waka-readme-stats](https://github.com/anmol098/waka-readme-stats) - 原项目作者及维护者。
* 所有为 `waka-readme-stats` 贡献的贡献者。

感谢所有让你的 README 更棒的人！
