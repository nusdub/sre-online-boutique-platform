# sre-online-boutique-platform
# 基于 Kubernetes 的微服务系统自动化发布与可观测性平台

## 项目背景

本项目基于 Online Boutique 微服务系统，构建一套面向 SRE 场景的 Kubernetes 应用交付与可观测性平台，覆盖应用部署、GitOps 发布、指标监控、日志采集、告警规则、故障演练和 Runbook 编写。

## 技术栈

- Linux
- Docker
- Kubernetes
- Kind
- Online Boutique
- Prometheus Operator
- Prometheus
- Grafana
- Alertmanager
- Loki
- Argo CD
- GitHub Actions
- Kustomize

## 系统架构

GitHub 仓库作为声明式配置源，Argo CD 监听仓库变化并自动同步 Kubernetes manifests 到集群；Online Boutique 运行在 prod namespace；Prometheus 采集 Kubernetes 与业务服务指标，Grafana 展示监控大盘，Alertmanager 负责告警，Loki 负责 Pod 日志采集与检索。

## 核心功能

1. Kubernetes 微服务部署
2. GitOps 自动化发布
3. Prometheus 指标采集
4. Grafana 监控大盘
5. Alertmanager 告警规则
6. Loki 日志检索
7. HTTP 可用性探测
8. 故障演练与服务恢复验证

## SLI / SLO

- SLI：frontend HTTP probe success rate
- SLO：最近 30 天可用性 >= 99%
- 告警：frontend 连续 1 分钟探测失败触发 critical 告警

## 故障演练

- frontend 副本数缩容为 0，验证 HTTP 探测失败与告警触发
- 删除 frontend Pod，验证 Deployment 自愈能力
- 创建 CPU 压力 Pod，验证 Prometheus 资源指标采集
