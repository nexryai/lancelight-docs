---
title: General Settings
weight: 2
next: /docs/port
prev: /docs
---

### default
```yaml
default:
  allowAllIn: false
  allowAllOut: false
  allowAllFwd: false
  allowPing: true
  enableIPv6: true
  enableLogging: true
```

#### `allowAllIn` (廃止予定)
これは絶対にfalseに設定してください。trueにすると全ての着信接続が許可されます。

#### `allowAllOut`
trueに設定してください。falseにすると発信接続できなくなります。

#### `allowAllFwd` (廃止予定)
フォワードをデフォルトで許可するかを定義します。Docker使用時などを除いてtrueにしないでください。

#### `allowPing`
pingを許可するかどうか

#### `enableIPv6`
 - ルーター広告など、IPv6の接続に必要な着信接続が許可されます。
 - 必要な場合にIPv6関係のルールを適用するようになります。

#### `enableLogging`
ログを有効にします。通報機能や統計機能を有効にする際に必要です。

### security
```yaml
security:
  alwaysDenyIP: ["1.1.1.1"]
  alwaysDenyASN: ["53667", "397702"]
  alwaysDenyTor: true
  disablePortScanProtection: false
```

#### `alwaysDenyIP` `alwaysDenyASN`
設定したIPアドレス、ASNからの全ての着信接続を破棄します。

#### `alwaysDenyTor`
Torの出口ノードからの着信接続を全て破棄します。

#### `disablePortScanProtection`
TCP NULLやTCP XMASポートスキャンを検知してブロックする機能を無効にします。
