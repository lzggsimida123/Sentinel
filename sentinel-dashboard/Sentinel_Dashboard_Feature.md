# Sentinel控制台功能介绍

## 0. 概述

Sentinel控制台是流量控制、熔断降级规则统一配置和管理的入口，它为用户提供了机器自发现、簇点链路自发现、监控、规则配置等功能。在Sentinel控制台上，我们可以配置规则并实时查看流量控制效果。使用Sentinel控制台的流程如下：

```
客户端接入 -> 机器自发现 -> 查看簇点链路 -> 配置流控规则 -> 查看流控效果
```

## 1. 功能介绍

### 1.1 机器自发现

Sentinel提供内置的机器自发现功能，无需依赖第三方服务发现组件即可实现客户端的发现。点击Sentinel控制台左侧导航栏的“机器列表”菜单，可查看集群机器数量和机器健康状况。

### 1.2 簇点链路自发现

Sentinel将每一个需要流控的URL或者接口称为一个资源，并使用URL地址或方法签名表示资源。Sentinel会自动发现所有潜在的资源和资源之间的调用链，并在“簇点链路”页面展示。资源是设置流控规则的载体，通过簇点链路自发现，可以方便的对重要资源设置流控规则、熔断降级规则等。

> 注意：客户端有访问量之后，才能在簇点链路页面看到资源监控。

### 1.3 实时监控

Sentinel监控功能能够实时查看集群中每个资源的实时访问以及流控情况。控制台左侧导航栏的“实时监控”菜单对应该功能。

### 1.4 流控降级规则设置

Sentinel提供了多种规则来保护系统的不同部分。流量控制规则用于保护服务提供方，熔断降级规则用于保护服务消费方，系统保护规则用于保护整个系统。

#### 1.4.1 流量控制规则

流量控制规则用于保护服务提供方，服务提供方指任何可以对外提供服务的系统，比如向终端用户提供Web服务的Web应用，向微服务消费方提供服务的Dubbo Service Provider等。系统的服务能力是有限的，如果消费方请求速度过高，则采用相应的保护策略，或是直接拒绝，或是排队等待。通过“流控规则”页面可以查看和配置流量控制规则。

#### 1.4.2 熔断降级规则

降级规则用于保护服务消费方。在微服务架构中，业务系统通常要依赖多个服务，依赖的某个服务不可用将会影响业务系统的可用性。解决这个问题的方法是及时发现服务的“不可用”状态，在调用时快速失败而不是等待调动超时或者重试。Sentinel通过熔断降级来达到快速失败的目的。通过“降级规则”页面可以查看和配置降级规则。

#### 1.4.3 系统保护规则

系统保护规则（简称`系统规则`）用于保护整个系统指标处于安全水位。无论是服务提供方还是消费方，活跃线程数过多、系统LOAD等过高都是系统处于高水位的指标。当系统水位过高时，系统应拒绝对外提供服务以便迅速降低资源占用。通过“系统规则”页面可以查看和设置系统保护规则。

## 2. 限制

本控制台只是用于演示Sentinel的基本能力和工作流程，并没有依赖生产环境中所必需的组件，比如**持久化的后端数据库、可靠的配置中心**等。目前Sentinel采用内存态的方式存储监控和规则数据，监控最长存储时间为5分钟，控制台重启后数据丢失。

更多：[Sentinel控制台启动和客户端接入](./README.md)。