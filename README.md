## 自用waka-readme-stats插件定制版
#### 修改内容：
  1. 修改了第一行标题出现ui渲染异常问题
  2. 新增了README_FILE 字段，控制更新的readme文件名称，可以用于多语言文件更新。
#### 使用示例：
   ```
   name: Waka Readme

on:
  schedule:
    # Runs at 12am IST
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

   #### 其他事项请参见官方github：[waka-readme-stats](https://github.com/anmol098/waka-readme-stats)

   #### 再次感谢原作者，感谢开源的力量。