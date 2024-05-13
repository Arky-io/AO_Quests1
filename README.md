# aoTheComputer

官方文档：https://cookbook_ao.g8way.io/


浏览器：https://www.ao.link/


推特：https://twitter.com/aoTheComputer


Discord:https://discord.gg/qWgGxJKwNJ


Quests 1"


奖励 500 AOCRED
 
# 一、启动AOS
## 1.安装NodeJS、AOS客户端及启动
以下内容将此窗口称为`窗口1`
```sh
apt-get update && apt install curl
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
nvm install 20
npm i -g https://get_ao.g8way.io
aos
```
 
 
# 二、消息传递 

## 1.发送消息
`process ID`修改为你的process ID

```lua
Send({ Target = "process ID", Data = "Hello World!" })
```

例：`Send({ Target = "gdC_YymKAxnCbliqR5TpAeJ5SaKFknKxIV_4n56pmHY", Data = "Hello World!" })`


![image](https://github.com/Arky-io/AO_Quests1/blob/main/IMG/process%20ID.png)


或者使用

```lua
Send({ Target = ao.id, Data = "Hello World!" })
```

反馈内容:`New Message From #你的process ID: Data = Hello World!`
 
## 2.存储 Morpheus 的ID变量

```lua
Morpheus = "wu_tAUDUveetQZpcN8UxHt51d9dyUkI4Z-MfQV8LnUU"
```
 
检查 Morpheus的process  ID变量

```lua
Morpheus
```

反馈内容:`wu_tAUDUveetQZpcN8UxHt51d9dyUkI4Z-MfQV8LnUU`
 
 
 
## 3.向 Morpheus 发送消息

```lua
Send({ Target = Morpheus, Data = "Morpheus?" })
```

反馈内容:`New Message From wu_...nUU: Data = I am here. You are f`


没有反馈需要等待一会，或者去Discord问一下是否是机器人正在维护中

## 4.查询收到几条消息

```lua
#Inbox
```

反馈内容:`3`反馈一个数字表示收到3条信息



## 5.查询最后后一条消息全部内容或者查看某条消息

```lua
 Inbox[#Inbox].Data
```

例：查看第3条信息` Inbox[3].Data`
反馈内容:`I am here. You are finally awake. Are you ready to see how far the rabbit hole goes?`

向 Morpheus 发送一条消息。

```lua
Send({ Target = Morpheus, Data = "Code: rabbithole", Action = "Unlock" })
```

反馈内容:`New Message wu_...nUU: Data = then let us test you`


使用Inbox[#Inbox].Data查看全部内容


`then let us test your readiness. create a chatroom and send me an invite. we will continue to see if you are truly ready there.`

# 三、建立一个聊天室
## 1.打开一个新的服务器窗口，创建`chatroom.lua`文件并编辑
以下内容将此窗口称为`窗口2`

```lua
nano chatroom.lua
```

编辑`chatroom.lua`文件

```lua
Members = Members or {}
```

`Ctrl+S`保存，`Ctrl+x`退出

![image](https://github.com/Arky-io/AO_Quests1/blob/main/IMG/chatroom.lua_1.png)


## 2.返回`窗口1`,加载`chatroom.lua`文件

```lua
.load chatroom.lua
```

反馈内容：`Loading...  chatroom.lua`

输入`Members`命令检查`chatroom.lua`是否加载成功

```lua
Members
```

反馈内容:`{  }`

## 3.创建聊天室功能
返回`窗口2`编辑`chatroom.lua`文件

```lua
nano chatroom.lua
```

反馈内容:`Loading...  chatroom.lua`

添加以下代码

```lua


  Handlers.add(
    "Register",
    Handlers.utils.hasMatchingTag("Action", "Register"),
    function (msg)
      table.insert(Members, msg.From)
      Handlers.utils.reply("registered")(msg)
    end
  )
```

`Ctrl+S`保存，`Ctrl+x`退出


![image](https://github.com/Arky-io/AO_Quests1/blob/main/IMG/chatroom.lua_2.png)

## 4.返回`窗口1`,加载`chatroom.lua`文件

```lua
.load chatroom.lua
```

反馈内容:`Loading...  chatroom.lua`

输入` Handlers.list`命令检查`chatroom.lua`是否加载成功

```lua
 Handlers.list
```

反馈内容:


![image](https://github.com/Arky-io/AO_Quests1/blob/main/IMG/Handlers.list%E5%8F%8D%E9%A6%88.png)


## 5.注册聊天室

``` lua
Send({ Target = ao.id, Action = "Register" })
```

反馈内容:`New Message From #你的process ID: Data = registered`

检查聊天室列表

```lua
 Members
```

反馈内容:`{ "#你的process ID" }`

## 6.添加广播处理程序

返回`窗口2`编辑`chatroom.lua`文件

```lua
nano chatroom.lua
```

添加以下代码

```lua

  Handlers.add(
    "Broadcast",
    Handlers.utils.hasMatchingTag("Action", "Broadcast"),
    function (msg)
      for _, recipient in ipairs(Members) do
        ao.send({Target = recipient, Data = msg.Data})
      end
      Handlers.utils.reply("Broadcasted.")(msg)
    end
  )
```

`Ctrl+S`保存，`Ctrl+x`退出


![image](https://github.com/Arky0420/AO-Quests_1/blob/main/IMG/chatroom.lua_3.png)

## 7.返回`窗口1`,加载`chatroom.lua`文件

```lua
.load chatroom.lua
```

反馈内容:`Loading...  chatroom.lua`

```lua
  Send({Target = ao.id, Action = "Broadcast", Data = "Broadcasting My 1st Message" })
```

反馈内容:


`New Message From #你的process ID: Data = Broadcasting My 1st `


`New Message From #你的process ID: Data = Broadcasted.`


## 8.邀请 Morpheus 加入聊天室

```lua
Send({ Target = Morpheus, Action = "Join" })
```

反馈内容:`New Message From Ydl...MPg: Data = Good. Very Good.  No`


没有反馈需要等待一会，或者去Discord问一下是否是机器人正在维护中


检查聊天室列表

```lua
 Members
```

反馈内容:`{ "#你的process ID", "wu_tAUDUveetQZpcN8UxHt51d9dyUkI4Z-MfQV8LnUU" }`

查看Morpheus反馈完整的信息

```lua
 Inbox[#Inbox].Data
```

反馈内容:`Good. Very Good.  Now, let me introduce you to Trinity.  Here is her process ID: y948iNUUNImam82gwZxFBNyvI8HLHB3Ld_uYmj9S20g. Once you have saved her process ID as you did mine, invite her to the chatroom, as well.`

## 9.存储 Trinity 的ID变量
上一步可看到Morpheus反馈Trinity的ID：`y948iNUUNImam82gwZxFBNyvI8HLHB3Ld_uYmj9S20g`

```lua
 Trinity = "y948iNUUNImam82gwZxFBNyvI8HLHB3Ld_uYmj9S20g"
```
 
检查  Trinity的process ID变量

```lua
 Trinity
```

反馈内容:`y948iNUUNImam82gwZxFBNyvI8HLHB3Ld_uYmj9S20g`

## 10.邀请 Trinity加入聊天室

```lua
 Send({ Target = Trinity, Action = "Join" })
```

反馈内容:`New Message From gdC...mHY: Data = So this is the one M`


没有反馈需要等待一会，或者去Discord问一下是否是机器人正在维护中


检查聊天室列表

```lua
 Members
```

反馈内容:`{ "#你的process ID", "wu_tAUDUveetQZpcN8UxHt51d9dyUkI4Z-MfQV8LnUU", "y948iNUUNImam82gwZxFBNyvI8HLHB3Ld_uYmj9S20g" }`

# 四、创建代币

## 1.创建一个蓝图代币

```lua
.load-blueprint token
```

查看新加载的处理程序

```lua
Handlers.list
```

## 2.生成代币

```lua
Send({ Target = ao.id, Action = "Info" })
```

反馈内容:`New Message From #你的process ID: Data = 5532`#5532数字是随机的

检查收到代币数量

```lua
Inbox[#Inbox].Data
```

反馈内容:`5532`#上一条消息反馈的数字

## 3.给 Trinity 发送代币

```lua
Send({ Target = ao.id, Action = "Transfer", Recipient = Trinity, Quantity = "1000"})
```

反馈：`Trinity: "Token received. Interesting. I wasn't sure you'd make it this far. I'm impressed, but we are not done yet. I want you to use this token to tokengate the chatroom. Do that, and then I will believe you could be the one."`

# 五、聊天室代币令牌门控

## 1.返回`窗口2`编辑`chatroom.lua`文件
下载库里面的`chatroom.lua`文件上传替换服务器的文件

或者返回`窗口2`编辑`chatroom.lua`文件

```lua
nano chatroom.lua
```

把最后一段Broadcast处理程序代码替换为以下代码

```lua

Handlers.add(
    "Broadcast",
    Handlers.utils.hasMatchingTag("Action", "Broadcast"),
    function(m)
        if Balances[m.From] == nil or tonumber(Balances[m.From]) < 1 then
            print("UNAUTH REQ: " .. m.From)
            return
        end
        local type = m.Type or "Normal"
        print("Broadcasting message from " .. m.From .. ". Content: " .. m.Data)
        for i = 1, #Members, 1 do
            ao.send({
                Target = Members[i],
                Action = "Broadcasted",
                Broadcaster = m.From,
                Data = m.Data
            })
        end
    end
)
```

`Ctrl+S`保存，`Ctrl+x`退出


![image](https://github.com/Arky0420/AO-Quests_1/blob/main/IMG/chatroom.lua_3.png)

## 2.返回`窗口1`
加载`chatroom.lua`文件

```lua
.load chatroom.lua
```

反馈内容：`Loading...  chatroom.lua`

## 3.测试聊天室代币令牌控制是否生效

```lua
Send({ Target = ao.id , Action = "Broadcast", Data = "Hello" })
```

反馈：`  `

## 4.打开一个新的服务器窗口,创建一个没有代币的AOS进程测试

以下将此窗口称为`窗口3`

```sh
aos chatroom-no-token
```

创建聊天室

```lua
.load chatroom.lua
```

反馈内容：`Loading...  chatroom.lua`

加入任务窗口聊天室，`process ID`修改为你的`窗口1`process  ID

```lua
Send({ Target = "process ID", Action = "Register" })
```

## 5.发送信息

`process ID`修改为你的`窗口1`process  ID

```lua
Send({ Target = "process ID" , Action = "Broadcast", Data = "Hello?" })
```

返回任务窗口等待反馈，反馈内容：` `

## 6.返回`窗口1`发送消息

```lua
Send({ Target = ao.id , Action = "Broadcast", Data = "It is done" })
```

等待反馈，反馈内容：` `

## 7.发送Claim信息

`Your-Discord-Username`改为你的`Discord ID`

```lua
Send({ Target = Trinity, Action = "Claim", Data = "Your-Discord-Username" })
```

进入AO Discord，找到`"q1-claims`频道，发送`窗口1`的process ID


# Quests 1完成


## 找到服务器中的`.aos.json`文件，下载`.aos.json`文件保存备份好！
## 找到服务器中的`.aos.json`文件，下载`.aos.json`文件保存备份好！！
## 找到服务器中的`.aos.json`文件，下载`.aos.json`文件保存备份好！！！


# `AOS`指令
查看完整的消息，替换`Inbox[#Inbox].Data`

```lua

Handlers.add(
    "PrintAnnouncements",
    Handlers.utils.hasMatchingTag("Action", "Announcement"),
    function(msg)
        print(msg.Data)
    end
)
```


将代码加入到`print_msg.lua`文件中，并在 `aos`运行


```lua
.load print_msg.lua
```


存储 `AOCRED` 代币的ID变量


```lua
CRED = "Sa0iBLPNyJQrwpTTG-tWLQU-1QeUAJA73DdxGGiKoJc"
```


查询 `AOCRED` 代币余额


```lua
Send({ Target = CRED, Action = "Balance"})
```


`.aos.json`文件是`aos`程序创建的钱包，可导入到Arweave钱包中


发送CRED代币到其他钱包，`your_address_here`改成你的钱包地址


```lua
 Send({ Target = CRED, Action = "Transfer", Recipient = "your_address_here", Quantity = "amount_here"})
```

