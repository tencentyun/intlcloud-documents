# 国际站发布动态公告

为提升非中国大陆地区的业务接入和防护能力配置体验，2022年6月2日， Web应用防火墙的产品能力全新升级，并上线Web2.0版本控制台。升级后，接入更稳定，防护能力更强大、流量管理支持更精细，并支持BOT行为管理和日志服务的增值能力；同时，控制台将增加中国大陆和非中国大陆地区划分，并支持通过地区切换控制切换，管理不同地区的实例资源。 

具体对不同类型的WAF实例影响如下：

- SAAS型WAF实例，WAF继续保持实例地域属性，系统自动根据地域字段增加地区字段，产品控制台区分地区管理，其他无变化。

- 负载均衡型WAF：中国大陆地区的WAF实例仅支持中国大陆CLB实例的web业务接入防护；非中国大陆地区的WAF实例仅支持非中国大陆CLB实例的web业务接入防护。

**本次** Web2.0升级后，您将获得以下产品能力和配置体验：

## 支持跨地区资源数据隔离


####  控制台将增加中国大陆和非中国大陆地区划分，并支持通过地区切换控制切换，详细如下图，支持在控制台菜单进行切换：

![](https://qcloudimg.tencent-cloud.cn/raw/b609ce00f74d56ffa5663501d0a1bc2e.png)
![](https://qcloudimg.tencent-cloud.cn/raw/5eefbaf3b13428f007001ce34da6fd68.png)
## 域名接入全面升级、更快捷

#### 域名接入和管理能力升级

**支持多实例统一管理，助力用户提升日常安全运维效率。**SAAS型WAF，IP回源支持用户自定义加权回源，满足复杂业务接入需求；域名回源支持多域名回源配置。

#### 域名接入向导支持

新增域名接入配置向导，完善域名添加后续步骤引导，贴心守护接入过程，业务接入更轻松。

#### 自定义流量标记

SAAS型WAF接入支持用户自定义流量标记能力，满足复杂的用户业务分析和联动防护诉求。

#### 客户端信息记录

SAAS型WAF支持用户自定义配置开启传递业务客户端的源 IP 地址和端口信息，补充 XFF 记录内容，助力金融、电商等行业客户业务监管合规。

## 防护能力升级

#### 一键开关防护

支持一键开启和关闭全部防护模块，以及部分防护功能模块的防护能力，助力用户快速处置日常运维过程中的业务问题排查，虽缩短定位周期，保障业务连续性。

#### 精细化流量管理

升级 IP 黑白名单为黑白名单管理，将原来自定义策略中处置动作为“放行”的规则升级为精准白名单规则，其他自定义策略规则升级为访问控制规则。规则本身的配置和执行效果不受升级影响。

通过精准白名单，支持用户日常安全运维的精细化流量管理，提升用户业务流量管控效率和效果，保证用户业务的安全性。

 

### 产品增值能力升级--BOT行为管理商业化发布

全新 BOT 一体化防护系统，联合前端对抗、威胁情报、以及大数据 AI 算法模型分析引擎三大防线，为用户提供基于风险度的流量可视化分析，构造威胁处置策略更加直观。