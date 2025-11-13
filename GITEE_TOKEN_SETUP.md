# Gitee 访问令牌配置指南

## 问题说明
GitHub Actions 工作流需要访问令牌才能推送到 Gitee 仓库。当前工作流已配置为使用 `GITEE_TOKEN` 密钥。

## 配置步骤

### 1. 获取 Gitee 访问令牌

1. 登录 [Gitee](https://gitee.com)
2. 点击右上角头像 → **设置**
3. 在左侧菜单中选择 **安全设置** → **私人令牌**
4. 点击 **生成新令牌**
5. 填写令牌信息：
   - **令牌描述**: `GitHub Actions Sync`
   - **权限**: 至少勾选 `projects` (仓库读写权限)
   - **过期时间**: 建议设置为较长时间（如 1 年）
6. 点击 **提交** 生成令牌
7. **重要**: 复制生成的令牌（只显示一次）

### 2. 在 GitHub 仓库中添加密钥

1. 进入你的 GitHub 仓库 (`caiweilv/DeltaForcePrice`)
2. 点击 **Settings** 标签页
3. 在左侧菜单中选择 **Secrets and variables** → **Actions**
4. 点击 **New repository secret**
5. 填写信息：
   - **Name**: `GITEE_TOKEN`
   - **Secret**: 粘贴刚才复制的 Gitee 访问令牌
6. 点击 **Add secret** 保存

### 3. 验证配置

配置完成后：
1. GitHub Actions 工作流将能够使用该令牌推送到 Gitee
2. 你可以在 GitHub Actions 页面查看工作流运行状态
3. 也可以手动触发工作流进行测试

## 安全注意事项

- 🔒 **不要将令牌提交到代码仓库**
- 🔒 **定期更换访问令牌**
- 🔒 **只授予必要的权限**
- 🔒 **如怀疑令牌泄露，立即撤销并重新生成**

## 工作流文件位置

当前工作流配置文件位于：`.github/workflows/sync-to-gitee.yml`

该文件已配置为：
- 每10分钟自动运行一次
- 支持手动触发
- 包含完整的错误处理和调试信息
- 使用 `GITEE_TOKEN` 进行 Gitee 认证

## 故障排除

如果工作流仍然失败：
1. 检查 Gitee 令牌是否有效
2. 确认 GitHub 仓库中的密钥名称是否为 `GITEE_TOKEN`
3. 验证令牌是否具有足够的权限
4. 查看 GitHub Actions 的详细错误日志