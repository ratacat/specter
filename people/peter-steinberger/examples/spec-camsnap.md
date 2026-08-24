<!-- source: https://github.com/steipete/camsnap/blob/main/docs/spec.md -->
## camsnap – CLI for RTSP/ONVIF cameras

### Goals (MVP)
- Add/list cameras with stored per-camera credentials.
- Grab a still (`snap`) or short clip (`clip`) from an RTSP URL.
- Skeleton for motion watch daemon (`watch`).
- ONVIF WS-Discovery; print ready-to-use `add` commands.

### Out of scope for MVP
- Tapo cloud login.
- Battery/low-power Tapo models that disable RTSP.
- Ubiquiti Protect API (planned; use RTSP URLs manually today).

### Command surface
- `camsnap add --name cam1 --host 192.168.1.50 --user tapo --pass secret`
- `camsnap list` — no passwords in output
- `camsnap snap --camera cam1 --out cam1.jpg [--timeout 5s]`
- `camsnap clip --camera cam1 --dur 10s`
- `camsnap discover` / `camsnap doctor` / `camsnap watch --camera cam1 --action "say motion"`
- `camsnap version`

### Architecture
- CLI: cobra in `cmd/camsnap`; subcommands in `internal/cli`
- Config: XDG YAML
- Media: ffmpeg wrappers with timeouts

### Data model (config.yaml)
```yaml
cameras:
  - name: porch
    host: 192.168.1.50
    port: 554
    protocol: rtsp
    username: tapo
    password: secret
```

### Security notes
Config local, unencrypted. Passwords never echoed in list output.

### Next steps after MVP
ONVIF auto-add, Ubiquiti Protect, gocv motion, ffmpeg preflight.
