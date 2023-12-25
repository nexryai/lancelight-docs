---
title: Port and IP Set Settings
weight: 3
next: /docs/outbound
prev: /docs/general
---

### ports
```yaml
ports:
  # Cloudflare経由での80ポートと443ポートへのアクセスを許可する。
  - port: 80
    allowIP: "cloudflare"

  - port: 443
    allowIP: "cloudflare"

  # 22ポートへの日本国からのTCPでのアクセスを許可する
  - port: 22
    proto: "tcp"
    allowCountry: "jp"

  # 3000ポートへのeth0への着信かつクライアントが192.168.1.0/24なアクセスを許可する
  - port: 3000
    allowIP: "192.168.1.0/24"
    allowInterface: "eth0"
```

#### `port` `proto`
許可するポートとプロトコル

#### `allowIP`
許可するIPアドレス。`cloudflare`に設定するとCloudflareのIPのみ許可されます。

#### `allowCountry` (v0.50以降のみ)
接続を許可する国

#### `allowInterface`
接続を許可するインターフェイス

### ipset
ipsetを定義します。

```yaml
ipset:
  - name: "TRUSTED"
    ip:
      - 192.168.1.100
      - 10.0.0.3

# 変数としてルール内で使えます
ports:
  - port: 80
    allowIP: "$TRUSTED"
```
