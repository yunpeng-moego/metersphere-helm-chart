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