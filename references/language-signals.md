# 分语言观察清单

本文件帮助主 skill 判断：不同语言里，哪些信号最能代表用户个人习惯。

## Java / Kotlin

重点观察：

- 包结构：按领域还是按分层
- 类名后缀：Service、Manager、Facade、Assembler、Converter、Handler、Config
- 接口与实现是否成对出现
- DTO / VO / Entity / BO 是否清晰分层
- 注解密度：Spring、Validation、Lombok、MapStruct 等
- 异常策略：checked / runtime、自定义异常、错误码
- 测试：JUnit 风格、测试类命名、fixture 组织
- 局部变量和参数名是否偏完整英文、缩写、拼音或 data/result/temp 这类泛名
- 复杂状态判断时更偏 switch、if-else、策略对象还是 Map 查表
- 在多人项目里，哪组文件占据入口、抽象基类、provider、meta、depends、topo 等核心链路

高价值信号：

- controller-service-repository 是否稳定薄厚分层
- mapping 是否显式放在 assembler / converter
- 是否偏好 builder、static factory、链式调用
- 是否存在一整组核心抽象文件呈现另一位稳定框架作者的手笔

## Python

重点观察：

- 包和模块命名是否严格 snake_case
- dataclass / pydantic / attrs / TypedDict 的偏好
- 类型注解密度和粒度
- docstring 是否存在、遵循何种格式
- 函数长度、是否偏好小私有辅助函数
- pytest 组织：fixture、parametrize、测试命名
- 是否爱写脚本式入口、if __name__ == "__main__"
- 局部变量名是语义化 snake_case 还是短名堆叠
- 控制流是早返回、match、if-elif 链还是字典分派
- 若项目多人协作，入口脚本、核心 package 初始化和调度层由谁主导

高价值信号：

- 边界层和领域层是否区分不同数据结构
- 是否偏好纯函数、小工具模块
- 注释更偏“why”还是几乎不写

## JavaScript / TypeScript

重点观察：

- 文件命名：camelCase、PascalCase、kebab-case
- export 风格：default 还是 named
- 类型放置：内联、集中、单独 types 文件
- React 结构：hooks/components/services/store/utils
- 状态管理：Context、Redux、Zustand、本地 state
- API 层封装粒度
- JSDoc / TSDoc 是否使用
- 是否使用 KubeJS 风格头注释，如 priority、side、requires
- 是否使用 class、function+prototype、对象字面量、全局单例中的哪一种或混合哪几种
- 局部变量偏好：tmp/data/obj/map/result 还是具象命名
- 分支偏好：switch、if-else 链、事件路由、查表分发
- 命名语言：标准英文、错拼英文、拼音、中文直译、混合命名
- 是否出现明显的 Vibe Coding / AI 强辅助区域，例如 DSL、转换器、兼容包装层、解释性注释密集区
- 哪些文件位于注册入口、共享对象、provider、metadata、loader、pack 分发等高中心性位置

高价值信号：

- 组件是否偏展示与容器分离
- hook 是否专注单一职责
- 是否避免 barrel file，还是大量使用 index 导出
- 是否通过共享对象、注册表、管理器来组织运行时状态
- 是否在脚本型项目中主动构造 API、Manager、Builder、Handler 分层
- 是否能区分“用户本人 KubeJS 脚本风格”“本人加 AI 的 DSL/转换层”“其他协作者的框架骨架风格”

## Go

重点观察：

- 包命名是否简短、语义是否稳定
- receiver 命名风格
- interface 是定义在消费方还是实现方
- 错误返回封装、wrap、sentinel error 使用方式
- 测试组织与 table-driven test 偏好
- 文件粒度：一个文件一个职责还是聚合
- 局部变量是否偏短名、err 链式复用，还是更具象
- 分支偏好是 if err return、switch、type switch 还是映射表
- 哪些包或文件位于核心接口、构造函数、调度与装配主链

高价值信号：

- 是否喜欢小接口
- 是否偏好显式构造函数 NewXxx
- context 传递和日志边界是否一致

## Rust

重点观察：

- module / crate 组织
- trait 抽象和 impl 位置
- Result / Option 处理方式
- anyhow / thiserror / eyre 等错误库偏好
- builder、newtype、enum 建模使用频率
- 测试模块和 feature gate 组织
- match、if let、while let 的偏好
- 局部变量是否偏语义化，还是大量复用 mut result/tmp/inner 这类中间名
- 哪些模块承担 crate 的抽象骨架、入口 glue 或 provider 式分发职责

高价值信号：

- 错误处理是快速传播还是局部消化
- 是否偏好强类型包装而不是裸字符串/整数

## C / C++

重点观察：

- 头文件与源文件分工
- 命名前缀、命名空间、宏命名
- RAII、智能指针、裸指针边界
- 模板使用意愿
- 注释是否主要用于约束、生命周期、线程安全说明
- 单元测试框架和 fixture 习惯
- 局部变量是否依赖前缀、缩写、领域黑话
- 分支和状态机是 switch 主导还是 if 链主导
- 哪些文件占据框架入口、资源管理骨架和统一适配层

高价值信号：

- 是否强调所有权和资源释放边界
- 是否偏保守封装，避免过度模板化

## C#

重点观察：

- namespace / folder 对齐关系
- record、class、interface 的使用边界
- async/await 命名和返回类型习惯
- dependency injection 注册方式
- DTO / Request / Response / Command / Query 切分
- XML 注释和单元测试组织
- 局部变量命名是否遵循完整英文或有项目缩写黑话
- 模式匹配 switch、if-else、LINQ、字典分发的使用偏好
- 哪些命名空间和目录承担应用主链、handler 骨架、registry 或 metadata 职责

高价值信号：

- 是否采用明显的 CQRS / MediatR 风格
- 是否在 application 层维持稳定的 request-handler 结构

## 通用判断提醒

以下信号跨语言都值得看：

- 是否偏好显式边界和清晰分层
- 是否热衷抽象，还是更重就地可读性
- 是否经常为复杂分支写解释性注释
- 是否喜欢把基础设施细节隔离在边缘
- 是否有稳定的测试命名和组织癖好
- 是否倾向标准英文命名，还是接受拼音、中文直译、错拼英文或多语混用
- 是否在函数内部偏爱早返回、switch、查表或顺序嵌套
- 是否存在稳定作者簇，而不是只有零星异常文件
- 哪些风格簇占据项目主链和高中心性位置，哪些只位于实验、包装或兼容层
- 是否应区分“用户本人稳定手写”“用户本人加 AI 强辅助”“其他人类协作者”“模板生成物”

但这些共性只能写在“跨语言共性”部分，不能替代具体语言画像。