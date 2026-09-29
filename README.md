# 青岛大学未来战队电控/视觉软件仓库索引

`index.yaml` 是 QDU-Robomaster 的 XRobot 模块源，地址为
<https://qdu-robomaster.github.io/qdu-future-modules/index.yaml>。`modules` 列出模块仓库，
`bsps` 列出 BSP 仓库（只用于发现，不作为模块依赖）。GitHub 地址给出包标识
`QDU-Robomaster/<仓库名>`。

## 使用

在 BSP 根目录把本源加入 `Modules/sources.yaml`：

```bash
xrobot source add-source https://qdu-robomaster.github.io/qdu-future-modules/index.yaml --priority 0
```

查询并使用模块：

```bash
xrobot source list --type module
xrobot source list --type bsp
xrobot source get QDU-Robomaster/RMMotor
xrobot module add QDU-Robomaster/RMMotor@same-or-dev
xrobot setup
```

输出示例：

```text
$ xrobot source list --type module
QDU-Robomaster/Aimer [module] https://github.com/QDU-Robomaster/Aimer.git
QDU-Robomaster/Arm [module] https://github.com/QDU-Robomaster/Arm.git
......
```

## 基础库

`modules` 列表同时包含可实例化的模块和只被其他模块依赖的基础库。基础库不能从列表中删除，否则依赖解析会失败。

基础库在自己的主头文件 manifest 中写 `standalone: false`（当前为 `Motor`、`CameraBase`、`VisionPreview`）：它们不能在应用配置中实例化，模块 CI 只编译其源码。`xrobot` 以 manifest 为准，不读取 `index.yaml` 中的 `module_metadata`。

## 添加模块

通过 PR 把仓库地址加入 `index.yaml` 的 `modules`。仓库需符合 XRobot 1.0 模块结构：主头文件 `Repo.hpp` 声明普通类 `Repo`，含 `MODULE MANIFEST V2`，CI 调用共享工作流 `xrobot-org/XRobot/.github/workflows/module-ci.yml`。见 <https://xrobot.work/docs/proj_man/proj-man-create-mod>。
