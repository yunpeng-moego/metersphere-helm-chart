# MeterSphere Helm Chart 部署

## 使用示例
```bash
helm install metersphere metersphere
```

## 配置环境变量

可以在 values.yaml 中为各个组件配置环境变量和 envFrom：

```yaml
# 全局环境变量，会应用到所有组件
common:
  env:
    - name: GLOBAL_ENV_VAR
      value: "global value"
  envFrom:
    - configMapRef:
        name: global-config

# 组件特定的环境变量
metersphere:
  env:
    - name: CUSTOM_ENV_VAR
      value: "custom value"
    - name: SECRET_VALUE
      valueFrom:
        secretKeyRef:
          name: my-secret
          key: secret-key
  envFrom:
    - configMapRef:
        name: my-configmap
    - secretRef:
        name: my-secret
```

支持的组件包括：
- metersphere
- resultHub
- taskRunner

组件特定的环境变量会追加到全局环境变量之后。

## 配置资源

可以在 values.yaml 中为各个组件配置资源请求和限制：

```yaml
# 全局资源设置，会应用到所有组件（除非组件有特定配置）
common:
  resources:
    limits:
      cpu: 1
      memory: 1Gi
    requests:
      cpu: 0.5
      memory: 512Mi

# 组件特定的资源设置
metersphere:
  resources:
    limits:
      cpu: 2
      memory: 2Gi
    requests:
      cpu: 1
      memory: 1Gi
```

组件特定的资源设置会覆盖全局资源设置。

### 默认资源配置

如果没有指定资源，将使用以下默认配置：

- MeterSphere 主应用:
  - Limits: 2 CPU, 2Gi 内存
  - Requests: 0.5 CPU, 512Mi 内存

- Result Hub 和 Task Runner:
  - Limits: 1 CPU, 1Gi 内存
  - Requests: 0.25 CPU, 256Mi 内存