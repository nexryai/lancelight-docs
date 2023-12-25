---
title: Router settings
weight: 5
prev: /docs/outbound
---

### router
{{< callout type="info" >}}
  ホームルーターを構築する時だけでなく、以下のような場合もこの機能を使用する必要があります。
   - トラフィックを中継するVPNサーバーの構築
   - LXDコンテナなどののホスト（ブリッジネットワーク使用時）
   - rootlessではないDockerの使用
{{< /callout >}}

```yaml
router:
  # ルーター機能を設定するかどうか
  configAsRouter: true

  # WAN側のインターフェイス
  wanInterface: "eth0"

  # プライベートネットワークのCIDRとインターフェイス
  # IPv6のアドレスを入れることでNAT66を有効にできます
  privateNetworks: ["192.168.10.0/24", "192.168.20.0/24", "fd11:0801::2/64"]
  lanInterfaces: ["eth1", "wg0"]

  # LAN内のデバイスに特定のDNSを強制する（AdGuard Home使用時などに有効）
  forceDNS: "192.168.0.1"

  # カスタムルート設定
  # LAN→WAN以外も許可したいとき（例えばVPNからLANへのアクセスを許可したい場合）などに使う
  customRoutes:
    - allowIP: "10.0.10.0/24"
      allowInterface: "wg1"
      allowDST: "192.168.10.0/24"
```

#### `configAsRouter`
ルーター機能を有効にします

#### `wanInterface`
ホストのWAN側として扱うインターフェイスを定義します

#### `privateNetworks` `lanInterfaces`
プライベートネットワークのCIDRとそのインターフェイスを設定します

#### `forceDNS`
{{< callout type="warning" >}}
  この機能はTailscaleのMagickDNSと互換性がありません。
{{< /callout >}}

LAN内のデバイスに指定したDNSの使用を強制します。
Pi-HoleやAdGuard Homeの使用時に役立ちます。



### nat (DNAT)
```yaml
nat:
  # wg0への10.0.0.0/24から10.0.0.1:53へのudpアクセスを192.168.1.100:53にDNATしたい場合
  - interface: "wg0"
    allowIP: "10.0.0.0/24"
    dstIP: "10.0.0.1"
    dstPort: "53"
    proto: "udp"
    natTo: "192.168.1.100:53"
```

#### `interface`
どのインターフェイスに着信したらNATするかを定義します

#### `allowIP`
許可するクライアントIPアドレス。全てのIPアドレスからのアクセスをNATしたい場合は`0.0.0.0/0`を設定します。（非推奨）

#### `dstIP`
宛先IPがどこに向いている場合にNATするかを定義します。
通常はこのデバイスのローカルIP、VPS環境などの場合はグローバルIPになります。

#### `dstPort` `proto`
どのポートにどのプロトコルで来たらNATするかを定義します。

#### `natTo`
NAT先を`[IPアドレス]:[ポート]`の形で設定します。
