name: Epic-YYDS
 
on:
  workflow_dispatch:
  schedule:
   # 定时执行可参考https://tool.lu/crontab
    - cron: 22 6 */3 * *
 
jobs:
  setup:
    env:
      #claim  --- 认领游戏商城周免游戏及其免费DLC
      #unreal --- 认领虚幻商城月免内容
      #get    --- 搬空游戏商城的免费游戏或免费DLC
      #默认指令为 python main.py claim 表示仅执行周免认领任务
      COMMAND: "python main.py claim"
      EPΙC_EMAΙL: ${{ secrets.EPIC_EMAIL }}
      EPΙC_PASSWΟRD: ${{ secrets.EPIC_PASSWORD }}
      PUSHER_TELEGRAM: ${{ secrets.PUSHER_TELEGRAM }}
      PLAYER: ${{ secrets.EPIC_PLAYER }}
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - uses: actions/setup-python@v3
      with:
        python-version: "3.10"
 
    - name: 拉取项目
      run: |
        git clone https://github.com/QIN2DIM/epic-awesome-gamer.git epic
 
    - name: 安装依赖
      run: |
        cd epic 
        pip install -r requirements.txt
        cd src
        cp config-sample.yaml config.yaml
        python main.py install
 
    - name: 开整
      run: |
        if [ -f "ctx_cookies.yaml" ];then cp ctx_cookies.yaml epic/src/database/cookies/; fi
        cd epic/src/ && ${{ env.COMMAND }}
