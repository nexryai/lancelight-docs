---
title: Getting Started
weight: 1
next: /docs/general

---

<!--more-->
### Dockerについて
{{< callout type="warning" >}}
  LanceLightとDocker、Podmanの互換性は保証されません。これはDockerがnftablesを自動的に上書きするためです。<br>
  Rootless DockerではNetwork namespaceが分離されるためこのような問題は発生しません。LanceLight環境でDockerを使用する際はDockerをRootlessにすることを強くおすすめします。
{{< /callout >}}

## Install with install script



#### Steps

{{% steps %}}

### Download

```shell
curl https://raw.githubusercontent.com/nexryai/lance-light/main/install.sh | sudo bash
```

### Create a config file
`/etc/lance.yml`

```yaml
default:
  allowAllIn: false
  allowAllOut: true
  allowAllFwd: false
  allowPing: true
  enableIPv6: true
  enableLogging: true

ports:
  - port: 80
    allowIP: "cloudflare"

  - port: 443
    allowIP: "cloudflare"

  - port: 22
    proto: "tcp"
```


### Enable firewall

{{< callout emoji="⚠" >}}
  有効にする前に、既存のファイアウォールを無効にしてください。
  切り替えの間無防備になることを避けるために、可能な限りルーターやVPSのファイアウォールでシステムを保護してください。
{{< /callout >}}

以下のコマンドを実行してファイアウォールルールを適用します。

```shell
sudo llfctl enable
```


### Start on boot
systemd経由で自動起動するようにします。

```shell
sudo systemctl enable lance
```

{{% /steps %}}

## 高度な設定を行う
{{< cards >}}
  {{< card link="general" title="基本設定" icon="code" >}}
  {{< card link="port" title="ポート設定とIP Set" icon="arrow-circle-right" >}}
  {{< card link="outbound" title="発信制限" icon="arrow-circle-left" >}}
  {{< card link="router" title="ルーターモードとNAT" icon="arrows-expand" >}}
{{< /cards >}}
