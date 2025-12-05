# BoxJS - 脚本工具箱

![](https://img.shields.io/badge/license-GPL-blueviolet.svg)
![GitHub release (latest by date)](https://img.shields.io/github/v/release/Bigzhangbig/boxjs?color=%23c694ff)

<image src="./BoxJS.gif" width="30%" height="55%">

## 📖 简介

BoxJS 是一个用于脚本管理和数据持久化的 Web 应用工具箱。它为 iOS 平台的脚本工具（如 Surge、Quantumult X、Loon、Stash 等）提供统一的数据管理和配置界面。

BoxJS 的核心功能包括：
- **应用订阅管理**：订阅第三方应用脚本
- **数据持久化**：统一管理脚本数据存储
- **会话切换**：支持多账号配置切换
- **备份与恢复**：数据备份和导入导出
- **可视化配置**：通过 Web 界面配置脚本参数

## 🚀 快速开始

### 安装 BoxJS

根据您使用的工具，选择对应的安装链接：

#### Surge
```
https://raw.githubusercontent.com/Bigzhangbig/boxjs/master/box/rewrite/boxjs.rewrite.surge.sgmodule
```

#### Quantumult X
```
https://raw.githubusercontent.com/Bigzhangbig/boxjs/master/box/rewrite/boxjs.rewrite.quanx.conf
```

#### Loon
```
https://raw.githubusercontent.com/Bigzhangbig/boxjs/master/box/rewrite/boxjs.rewrite.loon.plugin
```

#### Stash
```
https://raw.githubusercontent.com/Bigzhangbig/boxjs/master/box/rewrite/boxjs.rewrite.stash.stoverride
```

#### Shadowrocket
```
https://raw.githubusercontent.com/Bigzhangbig/boxjs/master/box/rewrite/boxjs.rewrite.surge.sgmodule
```

### 访问 BoxJS

安装完成后，在浏览器中访问：[http://boxjs.com](http://boxjs.com)

## 📚 开发文档

### BoxJS 内置应用支持的操作

BoxJS 提供以下核心操作接口：

#### 1. 数据存储操作

**读取数据**
```javascript
// 读取字符串数据
const value = $prefs.valueForKey(key)

// 读取 JSON 对象
const jsonValue = JSON.parse($prefs.valueForKey(key) || '{}')
```

**写入数据**
```javascript
// 写入字符串数据
$prefs.setValueForKey(value, key)

// 写入 JSON 对象
$prefs.setValueForKey(JSON.stringify(jsonObject), key)
```

**删除数据**
```javascript
$prefs.removeValueForKey(key)
```

#### 2. 会话管理

BoxJS 支持多账号配置切换功能：

```javascript
// 切换到指定会话
// 会话切换后，所有的数据读写都会基于当前会话
```

#### 3. 备份与恢复

- **备份当前数据**：将当前所有配置数据导出为 JSON 文件
- **恢复数据**：从 JSON 文件导入配置数据
- **多备份管理**：支持保存多个备份点

#### 4. 应用订阅

BoxJS 可以订阅第三方应用配置：

```javascript
// 订阅 URL 格式
https://your-domain.com/your-app-subscription.json
```

### JSON 订阅格式详解

#### 订阅文件结构

一个完整的 BoxJS 应用订阅文件包含以下结构：

```json
{
  "id": "your.app.sub",
  "name": "你的应用订阅",
  "author": "@your-name",
  "icon": "https://your-icon-url.com/icon.png",
  "repo": "https://github.com/your-username/your-repo",
  "apps": [
    {
      "id": "your.app.id",
      "name": "应用名称",
      "keys": ["data_key_1", "data_key_2"],
      "settings": [
        {
          "id": "setting_key",
          "name": "设置名称",
          "val": "默认值",
          "type": "text",
          "desc": "设置说明"
        }
      ],
      "author": "@author-name",
      "repo": "https://github.com/author/repo",
      "script": "https://raw.githubusercontent.com/author/repo/main/script.js",
      "icons": [
        "https://icon-url.com/icon-mini.png",
        "https://icon-url.com/icon-full.png"
      ]
    }
  ]
}
```

#### 字段说明

##### 订阅级别字段

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `id` | String | 是 | 订阅的唯一标识符，建议使用反向域名格式 |
| `name` | String | 是 | 订阅显示名称 |
| `author` | String | 否 | 订阅作者 |
| `icon` | String | 否 | 订阅图标 URL |
| `repo` | String | 否 | 订阅源代码仓库地址 |
| `apps` | Array | 是 | 应用列表 |

##### 应用级别字段

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `id` | String | 是 | 应用的唯一标识符 |
| `name` | String | 是 | 应用显示名称 |
| `keys` | Array | 是 | 应用使用的数据存储 key 列表 |
| `settings` | Array | 否 | 应用配置项 |
| `author` | String | 否 | 应用作者 |
| `repo` | String | 否 | 应用仓库地址 |
| `script` | String | 否 | 应用脚本 URL |
| `icons` | Array | 否 | 应用图标列表（推荐提供两个尺寸）|

##### 设置项字段

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `id` | String | 是 | 设置项的 key，用于数据存储 |
| `name` | String | 是 | 设置项显示名称 |
| `val` | Any | 是 | 默认值 |
| `type` | String | 是 | 类型：`text`, `textarea`, `number`, `boolean`, `checkboxes`, `radios`, `selects`, `slider` |
| `desc` | String | 否 | 设置项说明 |
| `placeholder` | String | 否 | 输入提示（仅文本类型）|
| `autoGrow` | Boolean | 否 | 自动增长（仅 textarea）|
| `rows` | Number | 否 | 行数（仅 textarea）|
| `items` | Array | 否 | 选项列表（checkboxes、radios、selects）|
| `min` | Number | 否 | 最小值（number、slider）|
| `max` | Number | 否 | 最大值（number、slider）|
| `step` | Number | 否 | 步进值（slider）|

### 订阅示例

#### 示例 1：简单应用

```json
{
  "id": "com.example.simple",
  "name": "简单应用示例",
  "author": "@example",
  "repo": "https://github.com/example/simple-app",
  "apps": [
    {
      "id": "simple.checkin",
      "name": "签到应用",
      "keys": ["simple_cookie", "simple_token"],
      "settings": [
        {
          "id": "simple_enable",
          "name": "启用签到",
          "val": true,
          "type": "boolean",
          "desc": "是否启用自动签到"
        },
        {
          "id": "simple_notify",
          "name": "推送通知",
          "val": true,
          "type": "boolean",
          "desc": "签到完成后是否推送通知"
        }
      ],
      "author": "@example",
      "repo": "https://github.com/example/simple-app",
      "script": "https://raw.githubusercontent.com/example/simple-app/main/checkin.js",
      "icons": [
        "https://example.com/icons/simple-mini.png",
        "https://example.com/icons/simple.png"
      ]
    }
  ]
}
```

#### 示例 2：复杂配置应用

```json
{
  "id": "com.example.advanced",
  "name": "高级应用示例",
  "author": "@example",
  "repo": "https://github.com/example/advanced-app",
  "apps": [
    {
      "id": "advanced.monitor",
      "name": "监控应用",
      "keys": ["adv_config", "adv_data", "adv_cache"],
      "settings": [
        {
          "id": "adv_mode",
          "name": "运行模式",
          "val": "normal",
          "type": "radios",
          "items": [
            {"key": "normal", "label": "普通模式"},
            {"key": "fast", "label": "快速模式"},
            {"key": "full", "label": "完整模式"}
          ],
          "desc": "选择脚本运行模式"
        },
        {
          "id": "adv_interval",
          "name": "检查间隔（分钟）",
          "val": 30,
          "type": "number",
          "min": 1,
          "max": 1440,
          "desc": "自动检查的时间间隔"
        },
        {
          "id": "adv_keywords",
          "name": "关键词列表",
          "val": "关键词1,关键词2,关键词3",
          "type": "textarea",
          "placeholder": "请输入关键词，用英文逗号分隔",
          "autoGrow": true,
          "rows": 5,
          "desc": "监控的关键词列表"
        },
        {
          "id": "adv_threshold",
          "name": "阈值设置",
          "val": 50,
          "type": "slider",
          "min": 0,
          "max": 100,
          "step": 5,
          "desc": "触发通知的阈值百分比"
        }
      ],
      "author": "@example",
      "repo": "https://github.com/example/advanced-app",
      "script": "https://raw.githubusercontent.com/example/advanced-app/main/monitor.js",
      "icons": [
        "https://example.com/icons/advanced-mini.png",
        "https://example.com/icons/advanced.png"
      ]
    }
  ]
}
```

## 🔧 在自己的应用中引用 BoxJS 操作

### 1. 使用 Env.js 封装库

BoxJS 提供了 `Env.js` 封装库，简化了跨平台脚本开发：

```javascript
// 在脚本开头引用 Env.js
const $ = new Env('你的脚本名称')

// 数据持久化操作
// 读取数据
const data = $.getdata('your_key')
const jsonData = $.getjson('your_json_key', {default: 'value'})

// 写入数据
$.setdata('value', 'your_key')
$.setjson({key: 'value'}, 'your_json_key')

// HTTP 请求（同步方式）
$.get('https://api.example.com/data', (error, response, data) => {
  if (error) {
    $.log(`请求失败: ${error}`)
  } else {
    $.log(`返回数据: ${data}`)
  }
})

// HTTP 请求（异步方式）
const response = await $.http.get('https://api.example.com/data')
const data = response.body

// POST 请求
const postData = await $.http.post({
  url: 'https://api.example.com/submit',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({key: 'value'})
})

// 通知
$.msg('标题', '副标题', '内容')

// 完成脚本
$.done()
```

### 2. 完整脚本示例

```javascript
/**
 * 示例签到脚本
 * 使用 BoxJS 进行数据持久化
 */

const $ = new Env('示例签到')

// 从 BoxJS 读取配置
const cookie = $.getdata('example_cookie')
const config = $.getjson('example_config', {
  enable: true,
  notify: true,
  interval: 24
})

// 主函数
!(async () => {
  if (!config.enable) {
    $.log('签到已禁用')
    return
  }

  if (!cookie) {
    $.msg('⚠️ 示例签到', '', '未找到 Cookie，请先获取')
    return
  }

  try {
    // 执行签到
    const result = await checkin()
    
    // 保存结果
    $.setjson(result, 'example_last_result')
    
    // 通知
    if (config.notify) {
      $.msg('✅ 签到成功', '', `获得积分: ${result.points}`)
    }
  } catch (e) {
    $.log(`❌ 签到失败: ${e}`)
    if (config.notify) {
      $.msg('❌ 签到失败', '', e.message)
    }
  }
})()
  .catch((e) => $.logErr(e))
  .finally(() => $.done())

// 签到函数
async function checkin() {
  const options = {
    url: 'https://api.example.com/checkin',
    headers: {
      'Cookie': cookie,
      'User-Agent': 'Mozilla/5.0'
    }
  }
  
  const response = await $.http.post(options)
  const data = JSON.parse(response.body)
  
  if (data.code === 0) {
    return {
      success: true,
      points: data.points,
      message: data.message
    }
  } else {
    throw new Error(data.message)
  }
}

// ====================
// Env.js 完整代码在此引用
// ====================
// prettier-ignore
function Env(t,e){/* Env.js 代码省略，实际使用时需要完整引用 */}
```

### 3. Cookie 获取脚本示例

```javascript
/**
 * Cookie 获取脚本
 */

const $ = new Env('示例 Cookie')

// 检查是否为 HTTP 响应
if (typeof $response !== 'undefined') {
  getCookie()
  $.done()
}

function getCookie() {
  const cookieName = 'example_cookie'
  const cookieValue = $request.headers['Cookie'] || $request.headers['cookie']
  
  if (cookieValue) {
    // 保存到 BoxJS
    $.setdata(cookieValue, cookieName)
    $.msg('✅ Cookie 获取成功', '', '可以关闭此页面')
    $.log(`Cookie: ${cookieValue}`)
  } else {
    $.msg('❌ Cookie 获取失败', '', '未找到 Cookie')
  }
}

// prettier-ignore
function Env(t,e){/* Env.js 代码 */}
```

## 📦 Env.js API 参考

### HTTP 请求方法

| 方法 | 说明 | 示例 |
|------|------|------|
| `$.get(url, callback)` | GET 请求（同步） | `$.get('https://api.com', (err, resp, data) => {})` |
| `$.post(url, callback)` | POST 请求（同步） | `$.post({url: 'https://api.com', body: 'data'}, callback)` |
| `$.http.get(options)` | GET 请求（异步） | `await $.http.get({url: 'https://api.com'})` |
| `$.http.post(options)` | POST 请求（异步） | `await $.http.post({url: 'https://api.com'})` |

### 数据持久化方法

| 方法 | 说明 | 返回值 |
|------|------|--------|
| `$.getdata(key)` | 读取字符串数据 | String |
| `$.setdata(val, key)` | 写入字符串数据 | Boolean |
| `$.getjson(key, defaultVal)` | 读取 JSON 对象 | Object |
| `$.setjson(val, key)` | 写入 JSON 对象 | Boolean |

### 通知方法

| 方法 | 说明 |
|------|------|
| `$.msg(title, subt, desc, opts)` | 发送通知 |
| `$.log(msg)` | 输出日志 |
| `$.logErr(err, msg)` | 输出错误日志 |

### 工具方法

| 方法 | 说明 |
|------|------|
| `$.time(fmt)` | 获取格式化时间 |
| `$.wait(millisec)` | 等待指定毫秒 |
| `$.done(val)` | 结束脚本 |

## 🔗 引用和订阅 BoxJS 应用

### 添加订阅

1. 打开 BoxJS Web 界面：[http://boxjs.com](http://boxjs.com)
2. 点击「订阅」菜单
3. 输入订阅链接
4. 点击「添加」

### 订阅链接格式

```
https://your-domain.com/your-subscription.json
```

### 常用订阅源

可以从 [chavyleung 应用订阅](https://github.com/chavyleung/scripts) 获取更多第三方应用脚本。

## 📝 开发建议

1. **使用唯一标识符**：为你的应用和设置项使用唯一的 ID，避免与其他应用冲突
2. **提供详细说明**：在 `desc` 字段中提供清晰的说明，帮助用户理解配置项
3. **设置合理默认值**：为所有配置项提供合理的默认值
4. **图标支持**：提供清晰的应用图标，建议两个尺寸（mini 和 normal）
5. **错误处理**：在脚本中添加完善的错误处理和日志输出
6. **通知提示**：关键操作完成后给用户发送通知
7. **数据验证**：从 BoxJS 读取数据后进行验证，确保数据有效性

## 🛠️ 安装 Env.js

### 用于集成
使用压缩版本：[Env.min.js](./Env.min.js)

### 便于阅读
使用完整版本：[Env.js](./Env.js)

### 使用方式

将 `Env.min.js` 的完整代码复制到你的脚本底部，然后在脚本开头调用：

```javascript
const $ = new Env('你的脚本名称')
```

## 📄 License

Copyright © 2019-present chavyleung. This project is [GPL](./LICENSE) licensed.

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 💬 讨论

Telegram 讨论组：[Chavy Scripts Group](https://t.me/chavyscripts)

## 🙏 赞助

感谢 [CloudFlare](https://www.cloudflare.com/) 提供支持
