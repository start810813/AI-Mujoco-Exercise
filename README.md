# AI-Mujoco-Exercise

----
## 環境設定
> 練習的開發環境為 Macbook pro 13"(無外接顯示卡)，以下安裝步驟適用於osx。windows的部分說明，僅供參考。

----
### 下載Mujoco
1. 請依照自己的電腦作業系統下載[mujoco](https://www.roboti.us/index.html)
> 我們使用200的版本(windows貌似只支援到150)，若下載不同版本的mujoco，以下設定路徑的資料夾名稱會不一樣，請注意並自行替換！
![image](picture or gif url)
2. 申請[簽證](https://www.roboti.us/license.html)，僅30天試用期。
![image](picture or gif url)
```shell
# 若Linux或Osx 下載getKey檔案時無法執行，試試看
# 先切到getid_osx所在資料夾
$ chmod 777 getid_osx
$ ./launch getid_osx
```
3. 登錄完成後會將mjkey.txt寄到信箱，請下載下來放到 ~/.mujoco 及 ~/.mujoco/mujoco200/bin這兩個位置
```shell
# 先切到mjkey.txt所在資料夾
$ cp mjkey.txt ~/.mujoco
$ cp mjkey.txt ~/.mujoco/mujoco200/bin
# 當然你也可以直接用文件管理器直接貼過去
```
4. 添加環境變數
> 在我的電腦中，使用bashrc 以及 zshrc，因此兩個都添加環境變數。使用vim文字編輯工具。
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
----
### 建立Anaconda環境
> 若你不需要建立虛擬環境，可以跳過。
```shell
$ conda create -n mujoco-gym python=3.6
$ conda activate mujoco-gym
```
----
### 安裝mujoco-py
```shell
$ cd /anaconda3/envs/mujoco-gym
$ git clone https://github.com/openai/mujoco-py.git
$ cd mujoco-py
$ pip install -e .
# 這裡若遇到錯誤，則缺什麼就裝什麼。
```
> windows的anaconda環境應在C:\Users\使用者名稱\anaconda3\envs\mujoco-gym
> windows的朋友請使用pip install mujoco-py==1.50.1.68，版本太新是無法使用的！這算是一個坑。
----
### 安裝GYM
1. 直接使用conda安裝 (當然也可以用pip)
```shell
$ conda install -c powerai gym
```
2. 到這邊就可以透過python去執行mujoco了！以下是測試程式碼
```python
import gym
env = gym.make('Humanoid-v2')
from gym import envs
print(envs.registry.all())    
print(env.action_space)
print(env.observation_space)
print(env.observation_space.high)
print(env.observation_space.low)
for i_episode in range(200):
   observation = env.reset()
   for t in range(100):
       env.render()
       print(observation)
       action = env.action_space.sample()    
       observation, reward, done, info = env.step(action)
       if done:
           print("Episode finished after {} timesteps".format(t+1))
           break
env.close()
```
----
### 安裝baselines套件
> baselines是由openAI開發的強化學習套件，裡面包含了多種的RL演算法，只需透過簡單的呼叫即可完成訓練。
1. 安裝CMake, OpenMPI and zlib
```shell
# Mac osx
$ brew install cmake openmpi
```
```shell
# Ubuntu
$ sudo apt-get update && sudo apt-get install cmake libopenmpi-dev python3-dev zlib1g-dev
```
2. 安裝baselines套件
```shell
# 若無tensorflow請先安裝
$ pip install tensorflow==1.14

# 下載baselines
$ pip install tensorflow==1.14
$ git clone https://github.com/openai/baselines.git
$ cd baselines
$ pip install -e .
```
> 到這裡就可以透過shell介面訓練mujoco了。但我們想在Jupyter notebook上執行，因此還要再下載stable-baselines套件。
3. 安裝stable-baselines套件
```shell
$ pip install stable-baselines[mpi]
```
----
### 到這裡就算全部安裝完成了！恭喜！
