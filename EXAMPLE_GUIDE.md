# BoxJS 示例订阅配置指南 - Example Subscription Configuration Guide

[English](#english) | [中文](#中文)

---

## 中文

### 简介

`example.boxjs.json` 是一个完整的 BoxJS 订阅配置示例文件，包含了 BoxJS 支持的所有功能和配置选项。本文件适合开发者学习和参考。

### 文件位置

```
/example.boxjs.json
```

### 订阅 URL

如果要在 BoxJS 中订阅此示例配置，可以使用以下 URL：

```
https://raw.githubusercontent.com/Bigzhangbig/boxjs/master/example.boxjs.json
```

### 包含的功能

#### 1. 订阅级别配置

- **id**: 订阅的唯一标识符
- **name**: 订阅显示名称（支持中英文）
- **author**: 作者信息
- **icon**: 订阅图标 URL
- **repo**: 代码仓库地址
- **description**: 订阅描述
- **onInstall**: 安装时触发的操作（支持 QuanX、Loon、Surge）

#### 2. 示例应用列表

本配置文件包含 6 个示例应用，分别演示不同的功能：

##### 应用 1：基础示例 (example.basic)
- 展示基本的配置项和数据存储功能
- 包含常用的开关和文本输入控件
- **设置项类型**：
  - `boolean`: 开关控件
  - `text`: 单行文本输入

##### 应用 2：高级示例 (example.advanced)
- 展示所有类型的设置控件
- 演示 HTML 描述功能
- 支持多个运行脚本
- **设置项类型**：
  - `text`: 单行文本输入
  - `textarea`: 多行文本输入（支持自动增长）
  - `number`: 数字输入（支持范围限制）
  - `boolean`: 开关控件
  - `radios`: 单选按钮组
  - `checkboxes`: 多选框组
  - `selects`: 下拉选择框
  - `slider`: 滑块控件
  - `colorpicker`: 颜色选择器

##### 应用 3：会话管理示例 (example.session)
- 展示多账号会话切换功能
- 演示会话数据的独立保存
- 适合需要管理多个账号的场景

##### 应用 4：通知配置示例 (example.notification)
- 展示各种通知配置选项
- 支持通知级别和声音设置
- 支持静默模式和勿扰时段

##### 应用 5：API 配置示例 (example.api)
- 展示 API 相关配置选项
- 支持自定义请求头和超时设置
- 演示缓存配置

##### 应用 6：动态选项示例 (example.dynamic)
- 展示从持久化数据中动态读取选项
- 演示 `@` 符号引用数据的用法
- 适合需要动态更新选项的场景

### 配置项类型详解

#### 文本类型

```json
{
  "id": "setting_key",
  "name": "设置名称",
  "val": "默认值",
  "type": "text",
  "placeholder": "输入提示",
  "desc": "设置说明"
}
```

#### 多行文本

```json
{
  "id": "setting_key",
  "name": "设置名称",
  "val": "默认值",
  "type": "textarea",
  "placeholder": "输入提示",
  "autoGrow": true,
  "rows": 5,
  "desc": "设置说明"
}
```

#### 数字类型

```json
{
  "id": "setting_key",
  "name": "设置名称",
  "val": 30,
  "type": "number",
  "min": 1,
  "max": 100,
  "desc": "设置说明"
}
```

#### 开关控件

```json
{
  "id": "setting_key",
  "name": "设置名称",
  "val": true,
  "type": "boolean",
  "desc": "设置说明"
}
```

#### 单选按钮组

```json
{
  "id": "setting_key",
  "name": "设置名称",
  "val": "option1",
  "type": "radios",
  "items": [
    { "key": "option1", "label": "选项一" },
    { "key": "option2", "label": "选项二" }
  ],
  "desc": "设置说明"
}
```

#### 多选框组

```json
{
  "id": "setting_key",
  "name": "设置名称",
  "val": ["feature1", "feature2"],
  "type": "checkboxes",
  "items": [
    { "key": "feature1", "label": "功能一" },
    { "key": "feature2", "label": "功能二" }
  ],
  "desc": "设置说明"
}
```

#### 下拉选择框

```json
{
  "id": "setting_key",
  "name": "设置名称",
  "val": "mode1",
  "type": "selects",
  "items": [
    { "key": "mode1", "label": "模式一" },
    { "key": "mode2", "label": "模式二" }
  ],
  "desc": "设置说明"
}
```

#### 滑块控件

```json
{
  "id": "setting_key",
  "name": "设置名称",
  "val": 50,
  "type": "slider",
  "min": 0,
  "max": 100,
  "step": 5,
  "desc": "设置说明"
}
```

#### 颜色选择器

```json
{
  "id": "setting_key",
  "name": "设置名称",
  "val": "#1E88E5",
  "type": "colorpicker",
  "desc": "设置说明"
}
```

### 高级特性

#### 1. onInstall 自动安装

```json
{
  "onInstall": {
    "title": "安装确认",
    "message": "是否需要自动安装相关资源？",
    "install": {
      "QuanX": "quantumult-x:///add-resource?...",
      "Loon": "loon://import?plugin=...",
      "Surge": "surge:///install-module?url=..."
    }
  }
}
```

#### 2. 多脚本支持

```json
{
  "scripts": [
    {
      "name": "主脚本",
      "script": "https://example.com/main.js"
    },
    {
      "name": "签到脚本",
      "script": "https://example.com/checkin.js"
    }
  ]
}
```

#### 3. HTML 描述

```json
{
  "desc_html": "<h3>标题</h3><p>内容</p>",
  "descs_html": [
    "<strong>功能一：</strong>说明",
    "<strong>功能二：</strong>说明"
  ]
}
```

#### 4. 动态选项

```json
{
  "type": "selects",
  "items": "@persistent_data_key"
}
```

#### 5. 脚本超时设置

```json
{
  "script_timeout": 30
}
```

### 使用建议

1. **唯一标识符**：为应用和设置项使用唯一的 ID，避免与其他应用冲突
2. **详细说明**：在 `desc` 字段中提供清晰的说明，帮助用户理解
3. **合理默认值**：为所有配置项提供合理的默认值
4. **图标支持**：提供清晰的应用图标，建议两个尺寸（mini 和 normal）
5. **错误处理**：在脚本中添加完善的错误处理
6. **数据验证**：从 BoxJS 读取数据后进行验证

### 开发流程

1. 复制 `example.boxjs.json` 作为模板
2. 修改订阅 ID、名称、作者等基本信息
3. 根据需求添加或删除应用
4. 为每个应用配置 keys 和 settings
5. 设置应用图标和脚本链接
6. 使用 prettier 格式化 JSON 文件
7. 发布到 GitHub 并生成订阅链接

### 测试订阅

在 BoxJS 中添加订阅：

1. 打开 BoxJS 界面
2. 进入「订阅」页面
3. 点击右上角「+」
4. 输入订阅 URL
5. 点击「添加」

---

## English

### Introduction

`example.boxjs.json` is a comprehensive BoxJS subscription configuration example file that contains all features and configuration options supported by BoxJS. This file is suitable for developers to learn and reference.

### File Location

```
/example.boxjs.json
```

### Subscription URL

To subscribe to this example configuration in BoxJS, use the following URL:

```
https://raw.githubusercontent.com/Bigzhangbig/boxjs/master/example.boxjs.json
```

### Included Features

#### 1. Subscription Level Configuration

- **id**: Unique identifier for the subscription
- **name**: Display name of the subscription (supports bilingual)
- **author**: Author information
- **icon**: Subscription icon URL
- **repo**: Repository address
- **description**: Subscription description
- **onInstall**: Actions triggered during installation (supports QuanX, Loon, Surge)

#### 2. Example Application List

This configuration file contains 6 example applications demonstrating different features:

##### App 1: Basic Example (example.basic)
- Demonstrates basic configuration and data storage
- Includes common switch and text input controls
- **Setting Types**:
  - `boolean`: Switch control
  - `text`: Single-line text input

##### App 2: Advanced Example (example.advanced)
- Demonstrates all types of setting controls
- Shows HTML description feature
- Supports multiple running scripts
- **Setting Types**:
  - `text`: Single-line text input
  - `textarea`: Multi-line text input (supports auto-grow)
  - `number`: Number input (supports range limits)
  - `boolean`: Switch control
  - `radios`: Radio button group
  - `checkboxes`: Checkbox group
  - `selects`: Select dropdown
  - `slider`: Slider control
  - `colorpicker`: Color picker

##### App 3: Session Management Example (example.session)
- Demonstrates multi-account session switching
- Shows independent session data storage
- Suitable for scenarios requiring multiple account management

##### App 4: Notification Configuration Example (example.notification)
- Demonstrates various notification configuration options
- Supports notification level and sound settings
- Supports silent mode and quiet hours

##### App 5: API Configuration Example (example.api)
- Demonstrates API-related configuration options
- Supports custom request headers and timeout settings
- Shows cache configuration

##### App 6: Dynamic Options Example (example.dynamic)
- Demonstrates dynamically reading options from persistent data
- Shows usage of `@` symbol for data reference
- Suitable for scenarios requiring dynamic option updates

### Configuration Type Details

All configuration types are detailed in the Chinese section above with JSON examples.

### Advanced Features

1. **onInstall Auto-installation**: Automatically install resources when subscribing
2. **Multiple Script Support**: Configure multiple running scripts for an app
3. **HTML Descriptions**: Use HTML for rich text descriptions
4. **Dynamic Options**: Reference persistent data using `@` symbol
5. **Script Timeout Settings**: Customize script execution timeout

### Usage Recommendations

1. **Unique Identifiers**: Use unique IDs for apps and settings to avoid conflicts
2. **Detailed Descriptions**: Provide clear descriptions in `desc` fields
3. **Reasonable Defaults**: Provide sensible default values for all configurations
4. **Icon Support**: Provide clear app icons, recommend two sizes (mini and normal)
5. **Error Handling**: Add comprehensive error handling in scripts
6. **Data Validation**: Validate data after reading from BoxJS

### Development Workflow

1. Copy `example.boxjs.json` as a template
2. Modify subscription ID, name, author, and other basic information
3. Add or remove apps as needed
4. Configure keys and settings for each app
5. Set app icons and script links
6. Format JSON file using prettier
7. Publish to GitHub and generate subscription link

### Testing Subscription

Add subscription in BoxJS:

1. Open BoxJS interface
2. Go to "Subscription" page
3. Click "+" in the top right corner
4. Enter subscription URL
5. Click "Add"

---

## 相关链接 - Related Links

- [BoxJS 官方仓库 - Official Repository](https://github.com/chavyleung/scripts)
- [BoxJS 文档 - Documentation](https://docs.boxjs.app)
- [更多订阅示例 - More Examples](https://github.com/chavyleung/scripts/tree/master/box)

---

## 许可证 - License

本示例文件遵循 [GPL License](../LICENSE)

This example file follows the [GPL License](../LICENSE)
