8# 5.15(GKI)-kernel-android13 for 多肉芋圆葡萄

**基于 Android13 GKI 内核 (5.15)**  
⚠️ 请仔细阅读完整文档后再进行操作 ⚠️

---

## 🚫 重要声明
- **内核源码为闭源项目**
- **严禁任何形式的逆向工程与二次分发**
- **不兼容任何ROOT解决方案**:
  - Magisk (官方/其他分支)
  - KernelSU (含NEX分支)
  - Apatch
  
## 📱 设备支持

### HyperOS 2.0 官方/第三方 ROM
- 小米13 / 小米13Pro / 小米13Ultra
- Redmi K60 Pro / Redmi K70

### HyperMod ROM 专属功能
- 游戏调度程序需搭配 HyperMod ROM 使用  
  **最低系统版本要求**: OS2.0.110.0

---

## ⚙️ 系统要求
- **Android 安全补丁**: ≥ 2024-12
- **推荐刷入工具**: [Kernel Flasher](https://github.com/capntrips/KernelFlasher)

---

## 🚀 内核特性

### 存储优化
- **F2FS 增强**:
  - 冷数据年龄轮询值优化
  - GC 脏段回收效率提升
  - I/O 优先级调整为 real-time 等级

### 内存管理
- **ZRAM 改进**:
  - 动态交换阈值调节
  - 后台应用驻留能力提升

### 游戏调度
- **帧率感知调度器**:
  - 实时帧率预测算法
  - 动态调整 CPU/GPU 资源分配
- **智能线程分配器**:
  - 基于前台负载的线程绑定
  - 支持 Vulkan/DX12 多线程渲染

### 功耗优化
- **空闲状态调节**:
  - CPU 空载功耗降低
  - 深度睡眠唤醒延迟优化
- **续航实测**:
  - 对比 HyperCore 提升 15% SOT
  - 旨提升续航表现 待机功耗
---

## 🔧 附加模块说明

### 游戏调度配置
| 设备型号           | ROM 要求                 | 功能特性                     |
|--------------------|--------------------------|------------------------------|
| 小米13 系列        | HyperMod ≥ OS2.0.110.0   | 动态渲染管线优化             |
| Redmi K60Pro / Redmi K70  | 官方 HyperOS 2.0         | 基础线程绑定                 |

- **其他ROM推荐调度器**:
  - Scene 调度
  - [fas-rs](https://github.com/shadow3aaa/fas-rs) (推荐)
  
---

## ⚠️ 已知冲突
| 模块类型           | 冲突表现                 | 解决方案                     |
|--------------------|--------------------------|------------------------------|
| 处理器限频模块     | FEAS 频率策略        | 移除所有 CPU 控制模块        |
| Asoulopt           | 线程调度优先级错乱       | 禁用/移除Asoulopt           |
| 线程优化           | 线程调度完全失效             | 禁用/移除线程优化      |
| scene｛核心分配｝           | 线程调度完全失效             | 禁用scene所有核心分配开关      |
| 系统处理器限频开关 | FEAS调度器异常 | 关闭处理器限频开关，重启设备      | 
---
## 🌟 疑惑解答
1. 为何ZRAM不遵循RAM:ZRAM(1:1)，我可以自己调配吗？
答: 因为1:1内存拓展在后台多开的实际情况下会导致卡顿阈值增加. 不建议自己修改分配ZRAM大小以及压缩算法. 附加模块默认调整大小为RAM大小+4，举个🌰子，我的RAM大小为12GB，+4之后就等于ZRAM大小(12+4)=16GB，16GB即ZRAM设定大小
-
2. 刷入内核和附加模块后，可以刷入其他Magisk模块保后台吗？
答: 附加模块已存在内存参数调优，与其他保后台，内存优化模块严重冲突. 
-
3.刷了内核和附加模块还是保不住后台怎么办？
答: 这里推荐使用焕晨大大的LSPosed模块: [AppRetentionHook](https://github.com/HChenX/AppRetentionHook)
-
4.是否建议使用第三方墓碑(NoActive)
答: HyperMod用户不推荐使用第三方墓碑，内核支持HyperOS2的zram队列冻结机制. QQ建议关闭自启动权限，设置-高级设置-应用扩展功能-电池优化-QQ-允许后台使用-(无限制)改为优化
不影响QQ的正常消息推送(QQ消息可以走Mipush推送)

---

## 📥 刷入指南
```bash
# 通过 Kernel Flasher 刷入
1. 下载 Pixel Kernel
2. 通过Kernel Flasher 刷入并重启设备
