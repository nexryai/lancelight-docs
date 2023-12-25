---
title: Outbound ACL
weight: 4
next: /docs/router
prev: /docs/port
---

### outbound
```yaml
outbound:
  compatibility:
    - tailscale
    - cloudflare_tunnel

  allowed:
    - dport: 53
      proto: "udp"

    - dport: 80
      proto: "tcp"

    - dport: 443
      proto: "tcp"

    - dport: 5432
      proto: "tcp"
      dstIP: "100.64.0.0/10"
```

#### `compatibility`
特定のアプリケーションとの互換性を保つためのルールを自動で追加します。
現在対応しているサービスは次の通りです。
| サービス | 設定ファイルでのvalue | 許可されるパケット |
| ---- | ---- | ---- |
| Cloudflared (Cloudflare Tunnel) |`cloudflare_tunnel`| 7844, 443 ポートへの発信 |
| Tailscale |`tailscale`| 3478, 41641 ポートへの発信 |


#### `allowed`
以下の条件**のすべて**を満たす発信パケットを許可します。
| key | 説明 |
| ---- | ---- |
| `dport` | 宛先ポート |
| `proto` | プロトコル |
| `dstIP` | 宛先のIPアドレス |
