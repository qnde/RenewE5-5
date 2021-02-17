# AutoApi v6.2.1 (2021-2-17) ———— E5自动续期
AutoApi系列：~~AutoApi(v1.0)~~、~~AutoApiSecret(v2.0)~~、~~AutoApiSR(v3.0)~~、~~AutoApiS(v4.0)~~、~~AutoApiP(v5.0)~~

## 说明 ##
* E5自动续期程序，但是**不保证续期**
* 设置了**周六日(UTC时间)不启动**自动调用，周1-5每6小时自动启动一次 （修改看教程）
* 调用api保活：
     * 查询系api：onedrive,outkook,notebook,site等
     * 创建系api: 自动发送邮件，上传文件，修改excel等
     
### 相关 ###
* AutoApi: https://github.com/wangziyingwen/AutoApi
* **错误及解决办法/续期相关知识/更新日志**：https://github.com/wangziyingwen/Autoapi-test
   * 大部分错误说明已更新进程序，详细请运行后看action日志报告
* 视频教程：
   * B站：https://www.bilibili.com/video/BV185411n7Mq/

## 步骤 ##
* 准备工具：
   * E5开发者账号（**非个人/私人账号**）
       * 管理员号 ———— 必选 
       * 子号 ———— 可选 （不清楚微软是否会统计子号的活跃度，想弄可选择性补充运行）    
   * 教程图片看不到请科学上网
   
* 步骤大纲：
   * 微软方面的准备工作 （获取应用id、密码、密钥）
   * GIHTHUB方面的准备工作  （获取Github密钥、设置secret）
   * 试运行
   
#### 微软方面的准备工作 ####

* **第一步，注册应用，获取应用id、secret**

    * 1）点击打开[应用注册页面](https://go.microsoft.com/fwlink/?linkid=2083908)，点击+**新注册**
    
     ![image](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApiP/creatapp.png)
    
    * 2）填入名字，“ 受支持账户类型 ”选第三个，“ 重定向url ”填入 https://login.microsoftonline.com/common/oauth2/nativeclient （不要按图片或者视频教程填，那是老版本的），点击**注册**
    
    ![image](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApiP/creatapp2.png)
    
    * 3）复制应用程序（客户端）ID到记事本备用(**获得了应用程序ID**！)，点击左边管理的**证书和密码**，点击+**新客户端密码**，点击添加，复制新客户端密码的**值**保存（**获得了应用程序密码**！）
    
    ![image](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApiP/creatapp3.png)
    
    ![image](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApiP/creatapp4.png)
    
* **第二步，获取refresh_token(微软密钥)**

    * 两种选择：
        * 下载项目里的GetToken.html文件；或者本地新建html后缀文档，把GetToken.html的内容复制到里面。然后本地打开，根据里面提示获取refresh_token.
        * 进入**[在线版](https://wangziyingwen.github.io/)**，根据提示获取refresh_token
               
    
    ![image](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApi/token地方.png)
    
 ___________________________________________________
 #### GITHUB方面的准备工作 ####

 * **第一步，fork本项目**
 
     登陆/新建github账号，回到本项目页面，点击右上角fork本项目的代码到你自己的账号，然后你账号下会出现一个一模一样的项目，接下来的操作均在你的这个项目下进行。
     
     ![image](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApi/fork.png)
     
 * **第二步，新建github密钥**
 
    * 1）进入你的个人设置页面 (右上角头像 Settings，不是仓库里的 Settings)，选择 Developer settings -> Personal access tokens -> Generate new token

    ![image](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApi/Settings.png)
    
    ![image](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApi/token.png)
    
    * 2）设置名字为 **GH_TOKEN** , 然后勾选repo，点击 Generate token ，最后**复制保存**生成的github密钥（**获得了github密钥**，一旦离开页面下次就看不到了！）
   
   ![image](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApiP/repo.png)
  
 * **第三步，新建secret**
 
    * 1）依次点击页面上栏右边的 Setting -> 左栏 Secrets -> 右上 New repository secret，新建6个secret： **GH_TOKEN、MS_TOKEN、CLIENT_ID、CLIENT_SECRET、CITY、EMAIL**  
   
    ![image](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApiP/setting.png)
    
    ![image](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApiP/secret2.png)
    
     **(以下填入内容注意前后不要有空格空行)**
 
     GH_TOKEN
     ```shell
     github密钥 (第三步获得)，例如获得的密钥是abc...xyz，则在secret页面直接粘贴进去，不用做任何修改，只需保证前后没有空格空行
     ```
     MS_TOKEN
     ```shell
     微软密钥（第二步获得的refresh_token）
     ```
     CLIENT_ID
     ```shell
     应用程序ID (第一步获得)
     ```
     CLIENT_SECRET
     ```shell
     应用程序密码 (第一步获得)
     ```
     CITY
     ```shell
     城市 (例如Beijing,自动发送天气邮件要用到)
     ```
     EMAIL
     ```shell
     收件邮箱 (自动发送天气邮件要用到)
     ```


________________________________________________

#### 试运行 ####

   * 1）点击上栏中间的Action进入运行日志页面，中间应该有个绿色按钮（I understand my workflow...），点击。
   
       自动刷新后，会看到左边有三个流程，一个Run api.Read，一个Run api.Write，一个Update Token。
       
         工作流程说明
             Run api.Write：创建系api，一天自动运行一次
             Run api.Read:  查询系api，每6小时自动运行一次
             Update Token： 微软密钥更新，每2天运行一次
             
       这三个流程名字前面应该是都有黄色感叹号的
   
       分别点进去，然后会看到有个黄条（this schedule was disabled......），点击 enable workflow 按钮，**三个流程都要按这个！**
   
       （不确定是否都需要进行这一步，我自己做视频教程的时候发现有的。如果你没有，直接忽略并往下进行，能正常运行就可以了 ）
   
   * 2）点击两次右上角的星星（star，就是fork按钮的隔壁）启动action，
   
        再点击上面的Action选择Run api.Read或者api.Write流程 -> build -> run api 就能看到每次的运行日志

       （必需点进去build里面的run api.XXX看下，api有没有调用到位，操作有没有成功，有没有出错）

        ![image](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApi/日志.png)
     
   * 3）再点两次星星，查看是否能再次成功运行
   
        然后点击Action里的 update token 流程 -> build -> update token ，日志里显示“微软密钥上传成功”。
       
        同时，依次点击页面上栏右边的 Setting -> 左栏 Secrets（也就是Github方面准备的第三步的secret页面），应该能看到MS_TOKEN显示刚刚update了
        
        （这一步是为了保证重新上传到secret的token是正确的）
    
        
#### 教程最后 ####

   程序会自行按计划启动，不必操心。
   
        但是github更新了防止薅羊毛的规则，如果仓库60天无任何变动，将会暂停Action，但是会发邮件通知，所以请留意邮箱，收到邮件请上来手动启动一下action。
       （我还没有收到过此邮件，但是据说邮件里会有启动链接，或者上来按两次星星按钮就行）
   
   **P版（AutoApiP）用户请留意是否会触发此暂停规则，由于P版采取了新方案，是否能跳过github检测活跃呢？如果P版收到暂停邮件，最好在issues的这个帖子[触发暂停统计](https://github.com/wangziyingwen/AutoApiP/issues/7)里留言**
   
   
### 教程完 ###

__________________________________________________________________________

## 额外设置 （看不懂请忽略）##
   * **定时启动修改**

   * **多账号/应用支持**
    
   * **超级参数设置**

#### 定时启动修改 ####
   
   我设定的每6小时自动运行一次（周六日不启动），每次调用3轮（点击右上角星星/star也可以立马调用一次），你们自行斟酌修改（我也不知道保持活跃要调用多少次、多久）：

  * 定时自动启动修改地方：在.github/workflow/autoapi.yml(只修改这一个)文件里，自行百度cron定时任务格式，最短每5分钟一次
   
   ![image](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApi/定时.png)
    
#### 多账号/应用支持 ####

   如果想输入第二账号或者应用，请按上述步骤获取**第二个应用的id、密码、微软密钥：**
 
   再按以下步骤：
 
   1)增加secret
 
   依次点击页面上栏右边的 Setting -> 左栏 Secrets -> 右上 New repository secret，新增加secret：APP_NUM、MS_TOKEN_2、CLIENT_ID_2、CLIENT_SECRET_2
 
   APP_NUM
   ```shell
   账号/应用数量(现在例如是两个账号/应用，就是2 ；3个账号就填3，日后如果想要增加请修改APP_NUM)
   ```
   MS_TOKEN_2
   ```shell
   第二个账号的微软密钥（第二步refresh_token），（第三个账号/应用就是MS_TOKEN_3，如此类推）
   ```
   CLIENT_ID_2
   ```shell
   第二个账号的应用程序ID (第一步获取),（第三个账号/应用就是CLIENT_ID_3，如此类推）
   ```
   CLIENT_SECRET_2
   ```shell
   第二个账号的应用程序密码 (第一步获取),（第三个账号/应用就是CLIENT_SECRET_3，如此类推）
   ```
   
   2)修改.github/workflows/里的两个yml文件（**超过5个账号需要更改，5个及以下暂时不用修改文件，忽略这一步**）
    
   yml文件我已经注明了，看着改就行，我已经写入5个账号模板了，跟着复制粘贴很简单的（没有找到比较好的自动方案）
  
#### 超级参数设置 ####
 
   ApiOfRead.py ， ApiOfWrite.py 文件第11左右行各有个config，具体参数设置已在文件里说明
   
   包括账号api的随机延时，api随机排序，每次轮数等参数
     
   
### 结尾 ###

有事发issue

Q群：[657581700](https://jq.qq.com/?_wv=1027&k=5FQJbWmV)  （项目相关讨论）

                              wangziyingwen
    




