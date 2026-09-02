# Changelog

## v8.0-vtumi-custom-1.3

### Added

- Added Yubico Authenticator CCID/OATH compatibility.
- Set the release firmware USB identity:
  - Manufacturer: `Yubico`
  - Product: `YubiKey OTP+FIDO+CCID`
  - VID: `0x1050`
  - PID: `0x0407`

### Verified

- FIDO2
- Passkey creation
- Passkey login
- Credential Management
- FIDO PIN / UV
- WebAuthn Commissioning
- CCID
- OATH
- OATH account enumeration
- TOTP calculation
- OATH account persistence after device replug
- Yubico Authenticator 7.4.1
- Yubico OTP

### SDK

- Repository: `pico-keys-sdk-vtumi-custom`
- Tag: `vtumi-custom-1.1`
- Commit: `794abaffa07fef3608bb0e636f30d241a08ddc25`

### Firmware

- Board: Waveshare RP2350 One
- MCU: RP2350
- Version: `v8.0-vtumi-custom-1.3`
- SHA256:

```text
9851be2df8b43895b21847b044d82226934098a76509924beb878936542b7b98
```
