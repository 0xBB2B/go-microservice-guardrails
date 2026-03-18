# 共享契约与代码生成

## 主题目标

让共享契约只有一个真源，并确保“谁拥有接口，谁拥有契约”，生成代码路径和运行时代码引用始终一致。

## 必须遵守

- 共享 proto 真源只放在 `contracts/proto/`
- 服务代码只消费 `contracts/gen/go/` 中的生成结果
- 目录按服务所有权组织，使用 `contracts/proto/service/v1/`
- proto package 使用 `service.v1`
- `go_package` 指向对应的生成代码路径
- 文件名表达接口职责，而不是调用关系
- 业务 request 只承载业务字段
- 服务身份和用户上下文字段通过 metadata 透传，不进入 proto request
- 修改 proto 后，同步更新 Buf 生成物、相关代码和测试

## 常见错误

- 在 `services/` 下长期维护另一份 proto 真源
- 调用方替被调用方定义接口字段语义
- `contracts/proto/`、`go_package`、生成目录三者不一致
- 把 `x-service-token`、`x-user-id` 之类上下文字段塞进业务 request
- 修改 proto 后只改真源，不更新生成物和依赖代码

## 落地检查点

- 新增接口时，目录和 package 是否符合服务所有权
- 生成代码路径是否与 `go_package` 一致
- 运行时代码是否只 import `contracts/gen/go/...`
- 业务字段和上下文字段是否分层
- proto 变更后，生成代码和测试是否一起更新
