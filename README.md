# <5.15(GKI)> for HyperOS/Android

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
| 其他冲突: 处理器限频开关 | FEAS调度器异常 | 关闭处理器限频开关，重启设备      | 

---

## 📥 刷入指南
```bash
# 通过 Kernel Flasher 刷入
1. 下载 Pixel Kernel
2. 通过Kernel Flasher 刷入并重启设备