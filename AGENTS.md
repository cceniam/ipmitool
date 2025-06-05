以下是调用SOL接口所需的所有核心文件：

## 核心实现文件

### 主要SOL库文件
- **`lib/ipmi_sol.c`** - SOL功能的核心实现，包含会话管理、激活/去激活、数据处理等 [1](#3-0) 

### 接口插件文件
- **`src/plugins/lanplus/lanplus.c`** - RMCP+接口实现，SOL功能的主要网络协议处理 [2](#3-1) 
- **`src/plugins/lan/lan.c`** - 传统LAN接口实现，包含SOL消息构建功能 [3](#3-2) 

### 头文件
- **`include/ipmitool/ipmi_sol.h`** - SOL相关的数据结构和函数声明
- **`include/ipmitool/ipmi_intf.h`** - 接口抽象层定义，包含SOL函数指针
- **`include/ipmitool/ipmi.h`** - 基础IPMI定义和常量
- **`include/ipmitool/helper.h`** - 通用辅助函数
- **`include/ipmitool/log.h`** - 日志记录功能

### 支持文件
- **`lib/ipmi_main.c`** - 主程序入口和命令分发 [4](#3-3) 
- **`lib/ipmi_tsol.c`** - Tyan SOL实现（特定厂商扩展） [5](#3-4) 
- **`src/plugins/ipmi_intf.c`** - 接口插件管理和加载

### LAN Plus协议支持文件
- **`src/plugins/lanplus/lanplus.h`** - LAN Plus接口头文件
- **`src/plugins/lanplus/lanplus_crypt.h`** - 加密功能定义
- **`src/plugins/lanplus/lanplus_crypt_impl.h`** - 加密实现
- **`src/plugins/lanplus/rmcp.h`** - RMCP协议定义
- **`src/plugins/lanplus/asf.h`** - ASF协议定义

## 编译依赖

要完整编译SOL功能，还需要：
- **OpenSSL库** - 用于RMCP+的加密功能
- **标准C库** - socket、select等系统调用
- **配置文件** - `config.h`（通过autotools生成）

## Notes

这些文件构成了完整的SOL实现栈。核心逻辑在`lib/ipmi_sol.c`中，网络协议处理在插件文件中，头文件提供接口定义。如果要在其他项目中集成SOL功能，建议重点关注这些文件的依赖关系和接口定义。
