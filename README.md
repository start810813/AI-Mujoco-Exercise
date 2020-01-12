# AI-Mujoco-Exercise

----
## 環境設定
> 練習的開發環境為 Macbook pro 13"(無外接顯示卡)，以下安裝步驟適用於osx。windows的部分說明，僅供參考。

----
### 下載Mujoco
1. 請依照自己的電腦作業系統下載[mujoco](https://www.roboti.us/index.html)
> 我們使用200的版本(windows貌似只支援到150)
![image](picture or gif url)
2. 申請[簽證](https://www.roboti.us/license.html)，僅30天試用期
![image](picture or gif url)
```shell
# 若Linux或Osx 下載getKey檔案時無法執行，試試看
$ chmod 777 getkey
$ ./launch getkey
```
3. 登錄完成後會將mjkey.txt寄到信箱，請下載下來放到 ~/.mujoco 及 ~/.mujoco/mujoco200/bin這兩個位置
```shell
$ cp mjkey.txt ~/.mujoco
$ cp mjkey.txt ~/.mujoco/mujoco200/bin
```
4. 添加環境變數
> 在我的電腦中，使用bashrc 以及 zshrc 因此兩個都添加環境變數。使用vim文字編輯工具。
```shell
$ sudo vim ~/.bashrc
$ sudo vim ~/.zshrc
# 貼上下面兩行
export LD_LIBRARY_PATH=/home/csy/.mujoco/mujoco200/bin${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
export MUJOCO_KEY_PATH=/home/csy/.mujoco${MUJOCO_KEY_PATH}
```
> windows的環境變數請至設定中尋找。主要是將/mjpro150/bin這一層的絕對路徑添加到PATH中。以及設定MUJOCO_KEY_PATH的絕對路徑(.txt檔)。
5. 測試Mujoco
```shell
$ cd ~/.mujoco/mujoco200/bin
$ ./simulate ../model/humanoid.xml
```
> 此時應會看到雙足機器人落下躺平。

