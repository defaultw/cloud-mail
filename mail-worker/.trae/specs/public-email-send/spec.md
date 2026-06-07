# 对外公开邮件发送接口 - 产品需求文档

## Overview
- **Summary**: 基于内部邮件服务方法开发一个对外公开的邮件发送接口，允许外部系统通过API发送邮件。
- **Purpose**: 提供安全、可靠的对外邮件发送能力，支持外部系统集成。
- **Target Users**: 外部系统开发者、系统集成商

## Goals
- 创建一个功能完整的对外邮件发送服务方法
- 在 public-service.js 中实现该方法
- 在 public-api.js 中注册公开API路径

## Non-Goals (Out of Scope)
- 不修改现有内部邮件服务逻辑
- 不添加新的数据库表结构
- 不改变现有用户认证机制

## Background & Context
- 内部邮件服务 `email-service.js` 已实现完整的邮件发送逻辑
- 公开服务 `public-service.js` 已有用户管理、token生成等方法
- 公开API `public-api.js` 已有 `/public/email/send` 路由但直接调用内部服务

## Functional Requirements
- **FR-1**: 在 `public-service.js` 中添加 `sendEmail` 方法
- **FR-2**: 方法需进行参数校验和安全验证
- **FR-3**: 在 `public-api.js` 中注册 `/public/email/send` 路由
- **FR-4**: 支持邮件主题、收件人、正文、附件等参数

## Non-Functional Requirements
- **NFR-1**: 接口需进行输入参数校验
- **NFR-2**: 需验证请求者身份（token验证）
- **NFR-3**: 返回统一的错误响应格式

## Constraints
- **Technical**: 基于现有的 Hono 框架和服务架构
- **Dependencies**: 依赖 email-service、verify-utils 等现有模块

## Assumptions
- 内部邮件服务 `emailService.send` 方法稳定可用
- 公开API需要的认证token机制已存在

## Acceptance Criteria

### AC-1: 公开服务方法创建
- **Given**: public-service.js 已存在
- **When**: 添加 sendEmail 方法
- **Then**: 方法能正确调用内部 emailService.send
- **Verification**: `programmatic`

### AC-2: 参数校验实现
- **Given**: 调用 sendEmail 方法
- **When**: 传入无效参数（如空收件人、空主题）
- **Then**: 返回错误响应
- **Verification**: `programmatic`

### AC-3: API路由注册
- **Given**: public-api.js 已存在
- **When**: 注册 `/public/email/send` 路由
- **Then**: 路由能正确响应请求
- **Verification**: `programmatic`

## Open Questions
- [ ] 是否需要添加额外的认证机制？
- [ ] 是否需要限制公开接口的发送频率？