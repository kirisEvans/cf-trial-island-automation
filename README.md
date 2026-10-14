# CF Trial Island Automation

面向 Windows 的《穿越火线》试炼岛本地键鼠自动化工具。程序启动后会打开一个本地控制台，提供“卡片投放”和“自动攻击”两个独立功能页。

> 本项目仅用于学习与交流。使用前请了解并遵守游戏用户协议、相关规则与法律法规，使用风险由使用者自行承担。

## 功能一览

### 无限循环投卡

- 设置 1～6 星卡片、卡片序号及游戏任务栏位置。
- 自动使用 `Win + 任务栏序号` 切换到游戏。
- 每轮依次执行：按一次 `E` → 选择卡片 → 点击“召唤 Boss”。
- 召唤后立即开始下一轮，不识别怪物状态，也不会自动打怪。
- 持续循环，直到手动停止或提交一组新设置。

### 自动攻击

- 设置游戏所在的任务栏位置。
- 自动切换到游戏并等待加载。
- 持续按住鼠标左键。
- 每 10 秒自动按一次 `F` 键。

### 任务控制

- 点击控制台右上角的 **停止当前任务** 可终止正在执行的任务。
- 无限投卡运行时，按 **空格键** 也可立即停止循环。
- 修改任意条件后再次点击启动，会先结束旧任务，再按新条件重新开始。
- 支持上传 JPG、PNG、WebP 作为控制台背景，或恢复默认壁纸。

## 环境要求

- Windows 10 / Windows 11
- Python 3.10 或更高版本
- 游戏使用与脚本坐标相匹配的界面布局；当前坐标基于 1920×1080 设计
- 游戏窗口不要被其他窗口遮挡

## 安装与启动

在项目目录打开 PowerShell：

```powershell
python -m pip install -r requirements.txt
python boss_automation_v2.py
```

脚本会请求管理员权限，请在 Windows 提示中允许。启动成功后会自动打开控制台页面。

## 使用说明

### 任务栏位置

“任务栏位置”指 Windows 任务栏从左到右的第几个图标，范围为 1～9。例如游戏位于第 4 个图标，控制台中应填写 `4`。

### 无限循环投卡

1. 打开 **卡片投放** 页。
2. 选择卡片星级、卡片序号和游戏任务栏位置。
3. 点击 **开始无限循环投卡**。
4. 需要停止时，点击右上角 **停止当前任务**，或按空格键。

### 自动攻击

1. 打开 **自动攻击** 页。
2. 填写游戏任务栏位置。
3. 点击 **启动自动攻击**。
4. 需要停止时，点击右上角 **停止当前任务**。

## 打包为文件夹版 EXE

先安装 PyInstaller：

```powershell
python -m pip install pyinstaller
```

再在项目根目录执行：

```powershell
python -m PyInstaller --noconfirm --clean --onedir --windowed --name BossAutomation --add-data "card_control_panel.html;." --add-data "card-wallpaper.png;." boss_automation_v2.py
```

打包完成后，程序位于：

```text
dist\BossAutomation\BossAutomation.exe
```

请保留整个 `BossAutomation` 文件夹，不要只复制其中的 `.exe` 文件。

## 常见问题

### 控制台显示“未连接”

请确认已启动 `boss_automation_v2.py` 或 `BossAutomation.exe`，再点击控制台中的启动按钮。

### 没有正确切换到游戏

检查任务栏位置是否准确。固定图标、其他运行程序或窗口顺序变化都可能影响位置。

### 点击位置不正确

确认游戏分辨率、系统缩放和游戏 UI 布局与脚本预设一致。当前卡片与按钮坐标按 1920×1080 界面设计。

## 目录说明

```text
boss_automation_v2.py     自动化主程序
card_control_panel.html   本地控制台页面
card-wallpaper.png        默认控制台壁纸
requirements.txt          Python 依赖列表
```
