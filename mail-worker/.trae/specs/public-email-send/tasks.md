# 对外公开邮件发送接口 - 实现计划

## [x] Task 1: 在 public-service.js 中添加 sendEmail 方法
- **Priority**: P0
- **Depends On**: None
- **Description**: 
  - 在 public-service.js 中添加 `sendEmail` 方法
  - 方法需要进行参数校验（收件人、主题必填）
  - 调用内部 emailService.send 完成邮件发送
- **Acceptance Criteria Addressed**: AC-1, AC-2
- **Test Requirements**:
  - `programmatic` TR-1.1: 方法能正确调用内部邮件服务
  - `programmatic` TR-1.2: 无效参数（空收件人/主题）返回错误
- **Notes**: 需要导入 emailService

## [x] Task 2: 在 public-api.js 中配置邮件发送路由
- **Priority**: P0
- **Depends On**: Task 1
- **Description**: 
  - 修改 `/public/email/send` 路由
  - 调用 publicService.sendEmail 方法
  - 返回统一响应格式
- **Acceptance Criteria Addressed**: AC-3
- **Test Requirements**:
  - `programmatic` TR-2.1: 路由能正确响应 POST 请求
  - `programmatic` TR-2.2: 返回结果格式符合预期

## [x] Task 3: 添加请求认证校验
- **Priority**: P1
- **Depends On**: Task 1
- **Description**: 
  - 在 sendEmail 方法中添加 token 认证校验
  - 验证请求的 token 是否有效
- **Acceptance Criteria Addressed**: NFR-2
- **Test Requirements**:
  - `programmatic` TR-3.1: 无效 token 返回 403 错误
  - `programmatic` TR-3.2: 有效 token 能正常发送邮件