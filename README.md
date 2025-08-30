# Shanhejian Visualization —— Backend

<br />
<div align="center" style="background: #fff; margin-bottom: 20px;">
<img src="./assets/s1.png" alt="Shanhejian Logo" width="100%" style="border-radius: 0px; box-shadow: 0 4px 8px rgba(0,0,0,0.1); margin-bottom: 20px"/>

English | [简体中文](./README.cn.md)
</div>
<br />
<div align="center">
<p><strong>Free Creation, What You See Is What You Get</strong></p>
  <p>You design, we generate source code and applications, ready to display, publish, or further develop.</p>
  
  [![Version](https://img.shields.io/badge/version-2.0.46-blue.svg)](https://github.com/your-org/open-shj-visual)
  [![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
  [![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey.svg)](https://shj.studio/website/)
  
  [🌐 Official Site](https://shj.studio/website/) | [📖 Docs](https://shj.studio/website/) | [💬 Community](https://github.com/your-org/open-shj-visual/discussions) | [🐛 Issues](https://github.com/your-org/open-shj-visual/issues)
</div>

## Overview

> Open Source Version Note: This open source version is mainly for learning and research purposes, providing complete data visualization features. commercial-grade source code export is only available in the [official online version](https://shj.studio/website/).

Shanhejian is an independent, domestically developed low-code 3D data visualization platform, dedicated to providing professional, efficient, and open data visualization solutions. Through visual drag-and-drop operations, data analysts, designers, and developers can easily create outstanding data visualization works, reducing weeks of traditional development to just hours. The platform is built on modern frontend technologies such as Vue 3, TypeScript, and Electron, supports team collaboration and custom component development, and is suitable for enterprise digitalization, government, education, and research scenarios.

## System Architecture

### 1. Overall Architecture

- **Layered Design**: Frontend (compatible with Vue/React, etc.), Backend (Spring Boot), Database (MySQL/PG/Oracle/DM/ClickHouse, etc.), WebSocket for real-time communication.
- **Modularization**: Each functional module is developed independently and deployed decoupled, facilitating maintenance and expansion.
- **Pluggable**: Data sources, visualization components, authentication, etc., all support plugin-based extensions.

### 2. Main Module Description

#### 2.1 shj-datasource (Data Source Module)

- **Function**: Responsible for unified access, configuration, connection management, data extraction, and permission isolation for all data sources (from dataease).
- **Supported Types**:
  - Relational Databases: MySQL, MariaDB, PostgreSQL, SQLServer, Oracle, ClickHouse, DM, etc.
  - File-based Data Sources: Excel, CSV, JSON
- **Core Capabilities**:
  - Data source registration, configuration, dynamic loading
  - Efficient management of database connection pools (Druid)
  - Pluggable Provider mechanism for easy extension of new data source types
  - SQL query, metadata (table/field) retrieval, data preview
  - File-based data source parsing and automatic field recognition
  - Team/user-level permission isolation
  - Support for multiple character sets and custom JDBC parameters

#### 2.2 shj-common (Common Module)

- **Content**: General utility classes, constants, exception handling, base entities, annotations, AOP, configuration, etc.
- **Purpose**: Provides basic capabilities and reusable components for business modules.

#### 2.3 shj-system (System Module)

- **Function**: System-level configuration, user and team management, permission control, logging, task scheduling, etc.
- **Highlights**: Supports multi-team collaboration, fine-grained permission allocation, flexible system parameter configuration.

#### 2.4 zerov-tools (Tools Module)

- **Content**: Third-party integration, authentication, file storage, auxiliary tools, etc.
- **Purpose**: Provides external capability expansion and convenient tools for the platform.

#### 2.5 shj-websocket (WebSocket Module)

- **Function**: Implements real-time communication between frontend and backend, supports message push, online collaboration, data change notifications, etc.

---

## Technology Stack

- **Backend**: Spring Boot, MyBatis-Plus, Druid, Gson/Fastjson
- **Database**: Supports MySQL, PostgreSQL, Oracle, DM, ClickHouse, etc.
- **Frontend**: Compatible with Vue, React, and other modern frontend frameworks
- **Communication Protocol**: RESTful API + WebSocket
- **Dependency Management**: Maven
- **Deployment**: Supports local, cloud, and containerized deployment

---

## Typical Business Processes

### 1. Data Source Registration and Management

1. Users/administrators fill in data source information (type, address, port, username, password, etc.) on the frontend page.
2. The backend zerov-datasource module receives the request, validates, and saves the data source configuration.
3. The system dynamically selects the corresponding Provider based on the data source type and establishes a connection through the Druid connection pool.
4. Supports operations such as add, delete, update, enable/disable, and permission allocation for data sources.

### 2. Data Query and Metadata Retrieval

1. Users select a data source and enter an SQL query or select a table.
2. The Provider executes the SQL and returns data results or table structure/field information.
3. Supports pagination, data preview, field permission filtering, etc.

### 3. File-based Data Source Processing

1. Users upload Excel/CSV/JSON files.
2. The system automatically parses the file content, recognizes fields, and previews data.
3. Supports field mapping, data cleaning, batch import, and other operations.

### 4. Multi-team/Multi-user Isolation

- Data sources, datasets, and visualization resources can be isolated and permission-controlled by team and user to ensure data security.

---

## Scalability and Customization

- **Data Source Extension**: Implement and register the Provider interface to support new data source types.
- **Visualization Component Extension**: Supports custom charts, dashboards, and other frontend components.
- **Authentication and Permissions**: Can integrate enterprise SSO, LDAP, OAuth2, and other authentication methods.
- **Third-party Integration**: Supports integration with external data platforms, storage, message queues, etc.

---

## Application Scenarios

- Enterprise-level data analysis and visualization
- Unified management and integration of multiple data sources
- Data development and data governance platforms
- BI reporting and dashboard building
- Data middle platform and data asset management

---

## Directory Structure (Example)

```
 shj_visual/
  ├─ zerov-common/      # Common module
  ├─ zerov-datasource/  # Data source module
  ├─ zerov-system/      # System module
  ├─ zerov-tools/       # Tools module
  ├─ zerov-websocket/   # WebSocket module
  └─ pom.xml            # Project aggregation configuration
```

---

## Quick Start

1. Clone the code repository and install dependencies
2. Configure the database and related parameters (application.yml/application-dev.yml)
3. Start the backend service (run the main class via Maven or IDE)
4. Access the frontend page to configure data sources and perform visualization operations

---

## Key Features

- Pluggable data source extension, supports custom Providers
- Multi-team/multi-user isolation with flexible permissions
- Efficient querying and caching for large data volumes
- Rich visualization capabilities and data modeling support
- Supports various file-based data sources, flexible data import/export

---

## Contact & Support

For custom development, technical support, or any suggestions, please contact the project maintainer or submit an issue.

---

For more detailed API documentation, developer guides, deployment instructions, or an English version of the documentation, please let us know!

## Third-party Configuration
- File upload uses Tencent Cloud; please configure it yourself in the tools module
- WeChat login also requires configuration
- SMS configuration

## Username/password
- 185111112222/Aa123456

## Community & Support

### Resources

- Official Wiki: [https://shjv.yuque.com/org-wiki-shjv-psfwkn/shj](https://shjv.yuque.com/org-wiki-shjv-psfwkn/shj)
- Official Docs: [https://shj.studio/website/](https://shj.studio/website/)
- Video Tutorials: Search "Shanhejian Visualization" on Bilibili


### Exchange

- QQ：795698425、805334126
- WeChat Community: Scan the QR code on the official site to join
- GitHub Discussions: Technical Q&A and discussions
- Zhihu: @Shanhejian Visualization
- Bilibili: @Shanhejian Visualization

<br />

<div style="display:flex; gap:4px;">
  <img src="./assets/q2.jpg" width="200px" style="border-radius: 0px; box-shadow: 0 2px 4px rgba(0,0,0,0.1)"/>
  <img src="./assets/q1.jpg" width="200px" style="border-radius: 0px; box-shadow: 0 2px 4px rgba(0,0,0,0.1)"/>
</div>

<br />
<br />

<div align="center">
  <p>If this project helps you, please give us a Star! ⭐⭐⭐</p>
  <p>Let's build a better data visualization ecosystem together! 🚀</p>
</div>