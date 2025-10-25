# MeterSphere Helm Chart 部署

## 使用示例
```bash
helm install metersphere metersphere
```

## 配置环境变量

可以在 values.yaml 中为各个组件配置环境变量和 envFrom：

```yaml
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