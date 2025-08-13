## Flipper Chat

Sub-GHz text messenger for Flipper Zero.

### Overview
- Point-to-point text messaging between two Flipper Zero devices over Sub-GHz.
- Frequencies: 433.92 MHz or 868.0 MHz.
- Modulation: OOK or GFSK.
- Payload: ASCII text.
- Integrity: CRC16-CCITT over header + payload.
- Retries on loss. Status indicators: Sent, Error, Received.

### UI
- Main menu: Send, Receive, Settings, History, Radio Info.
- Text input: T9 or alphanumeric via device buttons.
- Real-time message display.

### Security
- XOR encryption supported.
- AES not included.

### Storage
- History path: /ext/flipper_chat/history.dat
- Settings path: /ext/flipper_chat/settings.txt

### Protocol
- Preamble: 0xAA 0x55 0xAA 0x55 (4 bytes).
- Type: 1 byte (Text, File, Command, Ack, Nack).
- Message ID: 24-bit (3 bytes).
- Data: up to 128 bytes ASCII.
- CRC: 2 bytes CRC16-CCITT over header + data.

### Build (Flipper Build System)
- Prerequisite: flipperzero-firmware and fbt installed.
- Place this repo adjacent to flipperzero-firmware.
```bash
cd flipperzero-firmware
./fbt launch_app APPSRC=../flipper_chat/applications/flipper_chat
```

### Development (host-side helpers)
- Makefile provided for local structure checks and simple utilities. Not a device build.
```bash
make help
make run-tests
make run-example
```

### Configuration
- Frequency: 433920000 or 868000000 (Hz).
- Modulation: 0=OOK, 1=GFSK.
- Power: -30..+10 dBm (device dependent).
- Encryption: on/off, key up to 32 chars.
- Auto receive: on/off.
- Retry count: 1..3.

### Files
- applications/flipper_chat/*.c, *.h — app sources.
- applications/flipper_chat/application.fam — build descriptor.
- documentation/*.md — API, protocol, build notes.
- examples/basic_usage.c — example usage.
- tests/*.c — tests.

### Limitations
- ASCII-only payload.
- Point-to-point only.
- XOR provides minimal confidentiality.

### Regulatory
- Operate only on frequencies allowed in your jurisdiction.
- Respect duty cycle and power limits.

### License
- MIT.