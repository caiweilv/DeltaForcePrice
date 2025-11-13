# GitHub Actions 自动同步配置说明

## 概述
此工作流将每隔10分钟自动从 `orzice/DeltaForcePrice` GitHub仓库拉取最新代码，并同步到 `caiweilv/DeltaForcePrice` Gitee仓库。

## 工作流文件位置
`.github/workflows/sync-to-gitee.yml`

## 配置步骤

### 1. 在GitHub仓库中配置Secrets

需要在你的GitHub仓库 (`caiweilv/DeltaForcePrice`) 中添加以下Secret：

1. 进入GitHub仓库页面
2. 点击 `Settings` -> `Secrets and variables` -> `Actions`
3. 点击 `New repository secret`
4. 添加以下Secret：

#### GITEE_TOKEN
- **Name**: `GITEE_TOKEN`
- **Value**: 你的Gitee个人访问令牌

### 2. 获取Gitee个人访问令牌

1. 登录Gitee
2. 点击右上角头像 -> `设置`
3. 左侧菜单选择 `安全设置` -> `私人令牌`
4. 点击 `生成新令牌`
5. 设置令牌名称（如：GitHub Sync）
6. 选择权限：
   - `projects`: 读写权限
   - `pull_requests`: 读写权限
   - `issues`: 读写权限（可选）
7. 点击 `提交`，复制生成的令牌

⚠️ **重要**: 令牌只显示一次，请妥善保管！

### 3. 确保仓库权限

确保：
- 你对 `caiweilv/DeltaForcePrice` GitHub仓库有写入权限
- 你对 `caiweilv/DeltaForcePrice` Gitee仓库有写入权限

## 工作流功能

### 自动触发
- **定时触发**: 每10分钟运行一次 (cron: `*/10 * * * *`)
- **手动触发**: 可在GitHub Actions页面手动运行

### 执行步骤
1. **检出代码**: 从GitHub仓库检出完整代码
2. **配置Git**: 设置Git用户信息
3. **添加Gitee远程**: 配置Gitee仓库地址
4. **拉取最新**: 从upstream (orzice/DeltaForcePrice) 拉取最新更改
5. **推送到Gitee**: 将最新代码推送到Gitee仓库
6. **同步GitHub**: 确保GitHub仓库也是最新的

## 故障排除

### 常见问题

1. **GITEE_TOKEN权限不足**
   - 确保令牌有projects读写权限
   - 检查令牌是否已过期

2. **仓库不存在**
   - 确保Gitee仓库 `caiweilv/DeltaForcePrice` 已创建
   - 检查仓库路径是否正确

3. **网络问题**
   - GitHub Actions有超时限制，确保网络连接稳定
   - 检查仓库大小，过大可能导致超时

### 查看日志
在GitHub仓库的 `Actions` 标签页可以查看每次运行的详细日志。

## 手动测试

配置完成后，可以手动触发工作流进行测试：

1. 进入GitHub仓库的 `Actions` 页面
2. 选择 `Sync from GitHub to Gitee` 工作流
3. 点击 `Run workflow` 手动运行

## 注意事项

1. **API限制**: GitHub和Gitee都有API调用限制，10分钟间隔通常是安全的
2. **令牌安全**: 不要在代码中硬编码令牌，始终使用Secrets
3. **仓库大小**: 如果仓库很大，可能需要调整超时设置
4. **分支保护**: 如果有分支保护规则，可能需要调整工作流权限

## 监控建议

建议定期检查：
- 工作流是否正常运行
- Gitee仓库是否及时更新
- GitHub Actions的使用情况（避免超出免费额度）