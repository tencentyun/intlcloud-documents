The CLS console can be used in many ways, including logging in to the Tencent Cloud console, embedding it into the enterprise Ops system, deploying it independently, and accessing Grafana.

## Usage overview

| Usage         | Supported Features        | Free from Tencent Cloud Account Login      | Development Workload      | Account Permission Management       | Login State Conflict |
| -------------- | ---------------- | ------------------------------------ | ----------------------- | --------------------- | -------------------------- |
| [Tencent Cloud console](https://console.cloud.tencent.com/cls/overview) | All CLS features                           | No                                                   | None                                       | Tencent Cloud CAM         | /                          |
| [Iframe-embedded console - general embedding](https://intl.cloud.tencent.com/document/product/614/36997) | All CLS features                           | Yes, with iframe embedded into the enterprise Ops system for login through the authentication system | Light, where frontend iframe embedding is required                   | Enterprise authentication system              | Yes                     |
| Iframe-embedded console - SDK embedding | CLS features of log search and analysis and dashboard view     | Yes, with iframe embedded into the enterprise Ops system for login through the authentication system | Heavy, where frontend iframe embedding and backend access layer forwarding are required | Enterprise authentication system              | No                   |
| [Independently deployed console](https://www.tencentcloud.com/document/product/614/50280)                                           | All CLS features                           | Yes, with independent deployment and password-based or password-free login                   | None                                       | None or password authentication               | Yes                     |
| [Grafana plugin](https://intl.cloud.tencent.com/document/product/614/39592) | Grafana's dashboard features excluding alarming | Yes, with Grafana for data access                                | None                                       | Grafana's permission management system | No                   |




## Use cases

| Usage                  | Applicable Scenario                                                     |
| ------------------------- | ------------------------------------------------------------ |
| Tencent Cloud console              |-                                                            |
| Iframe-embedded console - general embedding | Scenarios where users are not supposed to log in to the Tencent Cloud console or have no Tencent Cloud accounts. CLS needs to be integrated into the enterprise Ops system. |
| Iframe-embedded console - SDK embedding  | Scenarios where users are not supposed to log in to the Tencent Cloud console or have no Tencent Cloud accounts. CLS needs to be integrated into the enterprise Ops system. Other accounts are needed to use the Tencent Cloud console. |
| Independently deployed console            | Scenarios where users are not supposed to log in to the Tencent Cloud console or have no Tencent Cloud accounts.     |
| Grafana plugin               | Scenarios where CLS needs to be integrated into the enterprise Grafana platform.                        |
