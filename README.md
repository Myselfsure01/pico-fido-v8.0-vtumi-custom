# Pico FIDO v8.0 VTUMI Custom

**Pico FIDO v8.0 VTUMI 定制版**

[English](#english) | [中文](#中文)

---

## English

### Overview

This project is a customized firmware based on [Pico FIDO](https://github.com/polhenarejos/pico-fido) v8.0.

It keeps the new v8.0 credential and storage architecture while restoring several device commissioning and PHY configuration capabilities from the earlier implementation.

### Main Changes

#### 1. Rollback

Removed the automatic rollback version injection from the build flow.

This allows custom firmware development and testing without automatically adding the rollback version metadata used by the upstream build configuration.

#### 2. WebAuthn Commissioning

Restored the `CommissionProfile` WebAuthn configuration mechanism.

The configuration profile is processed through:

```text
WebAuthn
    ↓
MakeCredential
    ↓
CommissionProfile
    ↓
phy_unserialize_data()
    ↓
phy_save()
```

Supported configuration items include:

- Product Name
- USB VID/PID
- LED Driver
- LED GPIO
- LED Brightness
- LED Mode
- Button Timeout
- ECC Curves
- PHY options

#### 3. PHY Configuration

Restored the following CTAP configuration commands:

```text
CTAP_CONFIG_PHY_VIDPID
CTAP_CONFIG_PHY_LED_GPIO
CTAP_CONFIG_PHY_LED_BTNESS
CTAP_CONFIG_PHY_OPTS
```

These commands are also reported through the `authenticatorConfig` capability list.

#### 4. USB Identity

Changed the USB Manufacturer string from:

```text
Pol Henarejos
```

to:

```text
Yubico
```

The USB Product Name can be customized through WebAuthn Commissioning.

#### 5. Custom Pico Keys SDK

This project uses the custom SDK:

```text
pico-keys-sdk-vtumi-custom
```

Repository:

https://github.com/Myselfsure01/pico-keys-sdk-vtumi-custom

### v8.0 Features Retained

The following v8.0 functionality remains in the project:

- Credential Management
- Object Store
- Resident Credentials
- Vault
- FIDO2
- WebAuthn
- Passkey
- FIDO PIN / UV
- Large Blob support
- OATH
- Yubico OTP
- CCID

The v8.0 credential and storage implementation was not replaced by the older v7.2 credential implementation.

### Tested

The current firmware has been tested with:

- FIDO2
- Passkey creation
- Passkey login
- Credential Management
- FIDO PIN / UV
- WebAuthn Commissioning
- Custom USB VID/PID
- Custom USB Product Name
- Yubico Authenticator
- Yubico OTP
- OATH

### Target Hardware

```text
MCU:   RP2350
Board: waveshare_rp2350_one
```

### Firmware

Current release:

```text
v8.0-vtumi-custom-1.1
```

Firmware file:

```text
pico_fido_v8.0_vtumi_custom.uf2
```

SHA256:

```text
334252b21b814f1283337738e04d2e6b9f1c6af36a3303157bc8fc55200dfe26
```

See the GitHub Releases page for the downloadable firmware.

### Build

```bash
git clone --recursive \
  git@github.com:Myselfsure01/pico-fido-v8.0-vtumi-custom.git

cd pico-fido-v8.0-vtumi-custom

git checkout v8.0-vtumi-custom-1.1
git submodule update --init --recursive

mkdir build
cd build

PICO_SDK_PATH=~/pico-sdk cmake .. \
  -DPICO_BOARD=waveshare_rp2350_one

cmake --build . -j$(nproc)
```

The resulting firmware is generated as:

```text
pico_fido.uf2
```

### Notes

This project is intended for development, research, and testing.

Do not enable Secure Boot or Hardware Lock features unless you fully understand the consequences and have a suitable recovery/development plan.

### License

This project is based on Pico FIDO and related open-source projects.

Please comply with the licenses of the upstream project and all third-party dependencies.

---

## 中文

### 项目简介

本项目基于 [Pico FIDO](https://github.com/polhenarejos/pico-fido) v8.0 进行定制开发。

在保留 v8.0 新版 Credential、Object Store、Vault 等架构的基础上，恢复了旧版本中的部分设备配置与 PHY 配置能力。

### 主要修改

#### 1. Rollback / 回滚

移除了构建流程中的自动 Rollback Version 注入。

这样在自定义固件开发和测试时，不会自动加入上游构建配置中的 Rollback Version 元数据。

#### 2. WebAuthn Commissioning / WebAuthn 设备配置

恢复 `CommissionProfile` WebAuthn 配置机制。

配置数据处理流程：

```text
WebAuthn
    ↓
MakeCredential
    ↓
CommissionProfile
    ↓
phy_unserialize_data()
    ↓
phy_save()
```

支持的配置项目包括：

- Product Name / 产品名称
- USB VID/PID
- LED Driver / LED 驱动
- LED GPIO
- LED Brightness / LED 亮度
- LED Mode / LED 模式
- Button Timeout / 按键超时
- ECC Curves / ECC 曲线
- PHY Options / PHY 参数

#### 3. PHY Configuration / PHY 配置

恢复以下 CTAP 配置命令：

```text
CTAP_CONFIG_PHY_VIDPID
CTAP_CONFIG_PHY_LED_GPIO
CTAP_CONFIG_PHY_LED_BTNESS
CTAP_CONFIG_PHY_OPTS
```

同时恢复这些配置在 `authenticatorConfig` 能力列表中的声明。

#### 4. USB Identity / USB 身份信息

将 USB Manufacturer 从：

```text
Pol Henarejos
```

修改为：

```text
Yubico
```

USB Product Name 可以通过 WebAuthn Commissioning 进行自定义。

#### 5. Custom Pico Keys SDK / 自定义 Pico Keys SDK

本项目使用自定义 SDK：

```text
pico-keys-sdk-vtumi-custom
```

仓库地址：

https://github.com/Myselfsure01/pico-keys-sdk-vtumi-custom

### 保留的 v8.0 功能

以下 v8.0 功能保持不变：

- Credential Management / 凭据管理
- Object Store / 对象存储
- Resident Credentials / 驻留凭据
- Vault
- FIDO2
- WebAuthn
- Passkey
- FIDO PIN / UV
- Large Blob
- OATH
- Yubico OTP
- CCID

本项目没有使用旧版 v7.2 的 Credential 实现替换 v8.0 的 Credential 和存储架构。

### 已测试

当前固件已经实际测试：

- FIDO2
- Passkey 创建
- Passkey 登录
- Credential Management
- FIDO PIN / UV
- WebAuthn Commissioning
- 自定义 USB VID/PID
- 自定义 USB Product Name
- Yubico Authenticator
- Yubico OTP
- OATH

### 硬件目标

```text
MCU：   RP2350
开发板：waveshare_rp2350_one
```

### 固件

当前版本：

```text
v8.0-vtumi-custom-1.1
```

固件文件：

```text
pico_fido_v8.0_vtumi_custom.uf2
```

SHA256：

```text
334252b21b814f1283337738e04d2e6b9f1c6af36a3303157bc8fc55200dfe26
```

可前往 GitHub Releases 下载已经编译好的固件。

### 编译

```bash
git clone --recursive \
  git@github.com:Myselfsure01/pico-fido-v8.0-vtumi-custom.git

cd pico-fido-v8.0-vtumi-custom

git checkout v8.0-vtumi-custom-1.1
git submodule update --init --recursive

mkdir build
cd build

PICO_SDK_PATH=~/pico-sdk cmake .. \
  -DPICO_BOARD=waveshare_rp2350_one

cmake --build . -j$(nproc)
```

编译完成后会生成：

```text
pico_fido.uf2
```

### 注意事项

本项目主要用于开发、研究和测试。

在启用 Secure Boot 或 Hardware Lock 等功能之前，请充分了解其工作机制和潜在后果，并准备好相应的恢复/开发方案。

### 许可证

本项目基于 Pico FIDO 及相关开源项目修改。

请遵守上游项目以及所有第三方依赖对应的许可证要求。

---

## Upstream / 上游项目

Pico FIDO:

https://github.com/polhenarejos/pico-fido

Pico Keys SDK:

https://github.com/polhenarejos/pico-keys-sdk

Custom Pico Keys SDK:

https://github.com/Myselfsure01/pico-keys-sdk-vtumi-custom

## Release / 发布版本

Current release / 当前版本：

**v8.0-vtumi-custom-1.1**
