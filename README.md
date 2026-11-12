# People Search PWA

一个适用于 iPhone Safari 的轻量级人物档案 PWA。静态网页文件部署到云端；人物资料和头像只保存在当前 iPhone 的 Safari IndexedDB 中。

## 功能
- 本机人物档案搜索（姓名、城市、职位、公司、行业）
- 新增、编辑、删除人物
- 从 iPhone 相册/相机选择头像；图片缩放压缩后保存在本机
- 网络搜索入口：把姓名交给 Google 搜索公开资料
- JSON 备份导出与导入
- Service Worker 缓存，支持首次加载后离线打开（需浏览器已成功缓存资源）

## 重要的数据边界
- 云端只托管 HTML/CSS/JS 等应用文件，不保存人物记录和头像。
- IndexedDB 数据绑定当前浏览器和设备。清除 Safari 网站数据、卸载/重置浏览器环境可能导致资料丢失。
- 私密浏览模式、浏览器存储配额或 iOS 系统清理可能影响持久性。定期使用“导出备份”。
- 这不是跨设备同步方案。换 iPhone 或换浏览器不会自动带走数据。
- “网络搜索”会将输入姓名发送给 Google；本机档案本身不会自动上传。

## 云端部署：GitHub Pages（免费静态托管）
1. 解压项目。
2. 在 GitHub 创建一个新仓库，例如 `people-search`。
3. 上传 `index.html`、`styles.css`、`app.js`、`manifest.webmanifest`、`sw.js` 和 `icons/`（README 可一并上传）。
4. GitHub 仓库打开 **Settings → Pages**。
5. 在 **Build and deployment** 中选择 **Deploy from a branch**。
6. Branch 选 `main`，目录选 `/ (root)`，保存。
7. 等待 GitHub Pages 发布，打开生成的 HTTPS 地址。

也可以使用 Netlify：将解压后的项目文件夹拖入 Netlify 的手动部署页面，获得 HTTPS 地址。

## 安装到 iPhone
1. 用 iPhone 的 Safari 打开部署后的 HTTPS 地址。
2. 点击底部“分享”。
3. 选择“添加到主屏幕”。
4. 如出现“作为 Web App 打开”，将其开启。
5. 点击“添加”，从主屏幕启动 People Search。

请使用 Safari 完成安装；不要使用普通浏览器标签页替代主屏幕 Web App 来测试离线能力。

## 本地测试
可在项目目录运行：
```bash
python -m http.server 8000
```
然后在同一网络下访问电脑 IP 的 `http://...:8000`。但 Service Worker 和 PWA 安装要求安全上下文，正式测试请使用 HTTPS 部署。

## 更新应用
更新代码后重新部署。Service Worker 缓存版本在 `sw.js` 中，将 `people-search-v1` 改成新版本号（例如 `people-search-v2`），让 iPhone 获取新资源。更新应用文件不会主动删除 IndexedDB 中的人物数据。

## 安全建议
- 设备设置 Face ID / 密码锁。
- 不要把导出的 JSON 备份发给无关人员。
- 仅登记必要、合法取得的商业联系信息；遵守 GDPR 等适用的数据保护要求。
