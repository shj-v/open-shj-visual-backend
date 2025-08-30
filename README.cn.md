# 山河鉴可视化 —— 后台

<br />
<div align="center" style="background: #fff; margin-bottom: 20px;">
<img src="./assets/s1.png" alt="山河鉴Logo" width="100%" style="border-radius: 0px; box-shadow: 0 4px 8px rgba(0,0,0,0.1); margin-bottom: 20px"/>

[English](./README.en.md) | 简体中文

</div>

<br />
<div align="center">
<p><strong>自由创作 所想所得</strong></p>
  <p>您设计，我们生成源码和应用程序，随时可以展示、发布或二次开发。</p>
  
  [![Version](https://img.shields.io/badge/version-2.0.46-blue.svg)](https://github.com/your-org/open-shj-visual)
  [![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
  [![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey.svg)](https://shj.studio/website/)
  
  [🌐 官网](https://shj.studio/website/) | [📖 文档](https://shj.studio/website/) | [💬 社区](https://github.com/your-org/open-shj-visual/discussions) | [🐛 反馈](https://github.com/your-org/open-shj-visual/issues)
</div>

## 介绍

> 当前组件库主要用于"山河鉴可视化"工具组件模块以及导出源码组件模块，包括100+组件、事件以及数据源。

山河鉴是一款自主可控、国产自研的低代码数据 3D 可视化工具，致力于为用户提供专业、高效、开放的数据可视化解决方案。通过可视化拖拽操作，让数据分析师、设计师、开发者都能轻松创建出色的数据可视化作品，将传统数周的开发工作压缩至数小时完成。工具基于 Vue 3 + TypeScript + Electron 等现代前端技术栈，支持团队协作、自定义组件开发，适用于企业数字化、政府数字化、教育科研等多种场景。


## 系统架构

### 1. 总体架构

- **分层设计**：前端（可对接 Vue/React 等）、后端（Spring Boot）、数据库（MySQL/PG/Oracle/DM/ClickHouse 等）、WebSocket 实时通信。
- **模块化**：各功能模块独立开发、解耦部署，便于维护和扩展。
- **插件化**：数据源、可视化组件、认证等均支持插件式扩展。

### 2. 主要模块说明

#### 2.1  shj-datasource（数据源模块）

- **功能**：负责所有数据源的统一接入、配置、连接管理、数据抽取与权限隔离来自dataease。
- **支持类型**：
  - 关系型数据库：MySQL、MariaDB、PostgreSQL、SQLServer、Oracle、ClickHouse、达梦（DM）等
  - 文件型数据源：Excel、CSV、JSON
- **核心能力**：
  - 数据源注册、配置、动态加载
  - 数据库连接池（Druid）高效管理
  - 插件化 Provider 机制，便于扩展新类型数据源
  - SQL 查询、元数据（表/字段）获取、数据预览
  - 文件型数据源解析与字段自动识别
  - 团队/用户级权限隔离
  - 支持多字符集、JDBC参数自定义

#### 2.2 shj-common（公共模块）

- **内容**：通用工具类、常量、异常处理、基础实体、注解、AOP、配置等。
- **作用**：为各业务模块提供基础能力和复用组件。

#### 2.3  shj-system（系统模块）

- **功能**：系统级配置、用户与团队管理、权限控制、日志、任务调度等。
- **亮点**：支持多团队协作、细粒度权限分配、系统参数灵活配置。

#### 2.4 zerov-tools（工具模块）

- **内容**：第三方集成、认证、文件存储、辅助工具等。
- **作用**：为平台提供外部能力扩展和便捷工具。

#### 2.5  shj-websocket（WebSocket模块）

- **功能**：实现前后端实时通信，支持消息推送、在线协作、数据变更通知等。

---

## 技术选型

- **后端**：Spring Boot、MyBatis-Plus、Druid、Gson/Fastjson
- **数据库**：支持 MySQL、PostgreSQL、Oracle、DM、ClickHouse 等
- **前端**：可对接 Vue、React 等现代前端框架
- **通信协议**：RESTful API + WebSocket
- **依赖管理**：Maven
- **部署方式**：支持本地、云端、容器化部署

---

## 典型业务流程

### 1. 数据源注册与管理

1. 用户/管理员在前端页面填写数据源信息（类型、地址、端口、用户名、密码等）。
2. 后端 zerov-datasource 模块接收请求，校验并保存数据源配置。
3. 系统根据数据源类型，动态选择对应 Provider，通过 Druid 连接池建立连接。
4. 支持对数据源的增删改查、启用禁用、权限分配等操作。

### 2. 数据查询与元数据获取

1. 用户选择数据源并输入 SQL 查询或选择表。
2. Provider 负责执行 SQL，返回数据结果或表结构、字段信息。
3. 支持分页、数据预览、字段权限过滤等。

### 3. 文件型数据源处理

1. 用户上传 Excel/CSV/JSON 文件。
2. 系统自动解析文件内容，识别字段、预览数据。
3. 支持字段映射、数据清洗、批量导入等操作。

### 4. 多团队/多用户隔离

- 数据源、数据集、可视化资源均可按团队、用户进行隔离和权限控制，保障数据安全。

---

## 扩展性与定制能力

- **数据源扩展**：只需实现 Provider 接口并注册，即可支持新类型数据源。
- **可视化组件扩展**：支持自定义图表、仪表盘等前端组件。
- **认证与权限**：可集成企业 SSO、LDAP、OAuth2 等多种认证方式。
- **第三方集成**：支持与外部数据平台、存储、消息队列等对接。

---

## 适用场景

- 企业级数据分析与可视化
- 多数据源统一管理与数据集成
- 数据开发、数据治理平台
- BI 报表、仪表盘搭建
- 数据中台、数据资产管理

---

## 目录结构（示例）

```
 shj_visual/
  ├─ zerov-common/      # 公共模块
  ├─ zerov-datasource/  # 数据源模块
  ├─ zerov-system/      # 系统模块
  ├─ zerov-tools/       # 工具模块
  ├─ zerov-websocket/   # WebSocket模块
  └─ pom.xml            # 项目聚合配置
```

---

## 快速开始

1. 克隆代码仓库，安装依赖
2. 配置数据库及相关参数（application.yml/application-dev.yml）
3. 启动后端服务（Maven 或 IDE 运行主类）
4. 访问前端页面，进行数据源配置和可视化操作

---

## 特色亮点

- 插件化数据源扩展，支持自定义 Provider
- 多团队/多用户隔离，权限灵活
- 支持大数据量高效查询与缓存
- 丰富的可视化能力与数据建模支持
- 支持多种文件型数据源，灵活的数据导入导出

---

## 联系方式与支持

如需定制开发、技术支持或有任何建议，请联系项目维护者或提交 issue。

---

如需更详细的接口文档、开发指南、部署说明或英文版文档，请随时告知！ 

## 第三方配置
- 文件上传使用的腾讯云的，请大家自己去配置在tools模块
- 微信登录也需要配置
- 短信配置

## 默认登录的账号密码
- 185111112222/Aa123456


## 社区与支持


### 资源

- 官方网站: [https://shjv.yuque.com/org-wiki-shjv-psfwkn/shj](https://shjv.yuque.com/org-wiki-shjv-psfwkn/shj)
- 官方文档: [https://shj.studio/website/](https://shj.studio/website/)
- 视频教程: B 站搜索"山河鉴可视化"

### 交流
- QQ群：795698425、805334126
- 微信社区: 扫描官网二维码加入
- GitHub Discussions: 技术讨论和问题解答
- 知乎: @山河鉴可视化
- B 站: @山河鉴可视化

<br />

<div style="display:flex; gap:4px;">
  <img src="./assets/q2.jpg" width="200px" style="border-radius: 0px; box-shadow: 0 2px 4px rgba(0,0,0,0.1)"/>
  <img src="./assets/q1.jpg" width="200px" style="border-radius: 0px; box-shadow: 0 2px 4px rgba(0,0,0,0.1)"/>
</div>

<br />
<br />

<div align="center">
  <p>如果这个项目对您有帮助，请给我们一个Star支持！⭐⭐⭐</p>
  <p>让我们一起构建更好的数据可视化生态！🚀</p>
</div>