## 客户介绍

腾讯互动娱乐事业群（IEG）旗下的腾讯游戏主打游戏开发和运营、网络游戏社区的机构。在游戏上云的道路上，腾讯互娱一直在不断探索、不断突破。2021年03月，腾讯互娱针对国际业务推出了在线游戏开发平台 PGOS，PGOS 提供：

- **后端服务平台：**PGOS（Proxima Game Online Service）是一种游戏在线服务解决方案，旨在降低游戏后端开发和维护难度，同时降低成本，从而使开发者专注于游戏玩法与核心逻辑开发。
- **全面托管服务：**借助完整的后端解决方案，消除了大规模构建，管理和运行服务器的挑战。即时自动扩缩容的专用服务器，为实时游戏提供低延迟和高可靠性。
- **一站式控制面板：**开发者及运维人员可以在 PGOS Web 门户上检索玩家信息及查看日志流水，监控实时数据并编辑相关服务配置。
- **跨平台 SDK：**提供开箱即用的 C++ SDK 和 UE4 插件，方便开发者在其游戏客户端和专有服务器中使用 PGOS 服务。
- **灵活的匹配规则：**为玩家提供在实时战斗中快速准确地与其他玩家进行匹配的能力。
- **扩展性和灵活性：**整个系统采用了微服务架构模式，而非具有不同层级的整体结构，使得开发人员可以添加和修改相应服务之间的交互。

## Serverless 解决方案

腾讯云 Serverless 天然支持上述 PGOS 提供的能力特性，PGOS 选择使用腾讯云 Serverless 技术提供底层计算支持，能够更好助力团队快速上云。

- **开箱即用：**用户无需额外购买、搭建和配置服务器，可完全专注于业务代码。这种架构方式不仅加快游戏发行和迭代速度，同时可降低运维成本，用户无需关注底层资源，腾讯云 Serverless 保障业务的稳定、安全和资源的可用。
- **动态扩缩容：**Serverless 的另一大特点是自动扩缩，轻松应对流量洪峰。在访问量突增时，自动扩容保障业务的正常运行。在流量低谷，自动缩容以节约成本。
- **实时监控：**腾讯云 Serverless 提供实时日志、监控面板，研发人员、管理人员可以实时监控业务运行状态，并且对接腾讯云云监控服务，提供运行时间、状态异常等多维度告警能力，使得问题可以在最短时间内被捕捉并且通知到用户。
- **扩展性和灵活性：**FaaS 的原子特性，天然支持业务灵活扩展。不同的云函数可支持独立的功能，既可支持函数间的相互调用又可独立更新和部署。同时支持函数代码在线编辑功能，从业务开发到部署再到监控，腾讯云 Serverless 提供了一站式的解决方案。
- **多种事件触发：**腾讯云 Serverless 支持约10种事件触发方式，包括定时触发器、API 网关触发器、对象存储触发器等等，满足用户多种触发场景的需求。

#### Serverless 为游戏上云提供算力支持的技术原理

腾讯云 Serverless 可以为国际业务 PGOS 提供底层运算支持，一个虚拟服务器（Virtual Server）对应一个或多个云函数，用户创建 Virtual Server 并编写对应的业务逻辑。PGOS 依赖 Serverless 提供完善的监控、日志能力，并对接后端服务，PGOS 更进一步封装 DevOps 工具，为用户提供全托管、自动构建和部署的功能。

<img src="https://main.qcloudimg.com/raw/8e45feb831d948d09ec66fb835d48715.png"/>

PGOS 提供多种驱动方式，底层对应不同的函数触发器来实现触发 Virtual Server 中业务的运行。

- **定时器驱动**：游戏可以在 Web Portal 上配置一个定时任务，定时触发 Virtual Server 的指定接口。
- **事件驱动**：Virtual Server 可以监听特定事件，当事件发生时自动触发 Vritual Server。
- **游戏驱动**：Game Client 或 DS 可以主动调用 Extension Interface，通过 Gateway 触发 Virtual Server 的指定接口。
- **手动驱动：**通过 Web Portal 手动运行/触发 Vritual Server 的指定接口。

<img src="https://main.qcloudimg.com/raw/bc4147b4356532827e9121320dc09a14.jpeg"/>

