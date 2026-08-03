# 青岛大学未来战队电控/视觉软件仓库索引

## 使用方式

### 添加源

```bash
xrobot_src_man add-source https://qdu-robomaster.github.io/qdu-future-modules/index.yaml
[SUCCESS] Added source: https://qdu-robomaster.github.io/qdu-future-modules/index.yaml to Modules\sources.yaml
```

### 列出软件包

```bash
xrobot_src_man list
Available modules:
  qdu-future/DR16                  source: https://qdu-robomaster.github.io/qdu-future-modules/index.yaml  (actual namespace: qdu-future)
......
```

## 独立构建契约

`index.yaml` 的 `modules` 列表同时包含可实例化应用和被其他模块依赖的基础库。基础库不能从列表中删除，否则依赖解析会失败。

自动化逐模块构建必须读取 `module_metadata`：当模块的 `standalone` 为 `false` 时，只验证源码可被依赖闭包包含，不为它自动生成 XRobot 应用实例。当前非独立模块为 `Motor`、`CameraBase` 和 `VisionPreview`。
