# Apache DevLake 部署验证 - Product Requirement Document

## Overview
- **Summary**: 按照项目文档说明部署 Apache DevLake 的数据库服务、后端服务及前端服务，确保所有服务组件能够成功启动并正常运行。
- **Purpose**: 验证 DevLake 项目的完整部署流程，确保开发环境可以正常运行，支持后续开发和测试工作。
- **Target Users**: 开发人员、测试人员

## Goals
- 成功启动数据库服务（MySQL）
- 成功构建并启动后端服务
- 成功构建并启动前端服务
- 验证所有服务能够正常运行，无错误日志输出
- 通过浏览器访问前端应用，验证页面能够正常加载

## Non-Goals (Out of Scope)
- 不涉及生产环境部署配置
- 不涉及 Helm/Kubernetes 部署方式
- 不涉及数据源插件的配置和数据同步

## Background & Context
根据项目文档，DevLake 使用 Docker Compose 进行本地开发环境部署，包含以下核心组件：
- MySQL 8.x - 数据库服务
- DevLake 后端 - Go 服务，运行在端口 8080
- Config UI - React 前端，运行在端口 4000
- Grafana - 可视化仪表盘，运行在端口 3002

## Functional Requirements
- **FR-1**: 数据库服务能够正常启动，接受连接
- **FR-2**: 后端服务能够正常启动，API 接口可访问
- **FR-3**: 前端服务能够正常启动，页面可访问
- **FR-4**: 所有服务无错误日志输出

## Non-Functional Requirements
- **NFR-1**: 服务启动时间应在合理范围内（< 2分钟）
- **NFR-2**: 服务应稳定运行，无崩溃或异常重启

## Constraints
- **Technical**: 需要 Docker/Docker Compose、Go、Node.js/Yarn
- **Dependencies**: 所有服务依赖 MySQL 数据库

## Assumptions
- 系统已安装 Docker 和 Docker Compose
- 系统已安装 Go 1.21+ 和 Node.js 18.x
- 所需端口（3306, 8080, 4000, 3002）未被占用

## Acceptance Criteria

### AC-1: MySQL 数据库服务启动成功
- **Given**: Docker Compose 配置文件已就绪
- **When**: 启动 MySQL 服务
- **Then**: MySQL 容器运行正常，端口 3306 可访问
- **Verification**: `programmatic`

### AC-2: 后端服务启动成功
- **Given**: MySQL 服务已启动
- **When**: 构建并启动后端服务
- **Then**: 后端服务运行在端口 8080，无错误日志
- **Verification**: `programmatic`

### AC-3: 前端服务启动成功
- **Given**: 后端服务已启动
- **When**: 安装依赖并启动前端服务
- **Then**: 前端服务运行在端口 4000，无错误日志
- **Verification**: `programmatic`

### AC-4: 前端页面可正常访问
- **Given**: 所有服务已启动
- **When**: 通过浏览器访问 http://localhost:4000
- **Then**: 页面正常加载，登录界面显示
- **Verification**: `human-judgment`

## Open Questions
- [ ] 是否需要验证 Grafana 服务？
- [ ] 是否需要测试具体的 API 接口？