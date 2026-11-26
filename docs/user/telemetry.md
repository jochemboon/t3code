# Telemetry and diagnostics

This build of T3 Code sends no telemetry. There are no product usage events, no install or device identifiers, no T3 Connect relay traces, and no mobile crash reports. Nothing about how you use the app leaves your machine unless you send it somewhere yourself.

Network traffic that remains is functional: your chosen providers, update checks, and, if you use them, T3 Connect and the mobile notification relay.

## Agent feedback

Optional tool for agents to write up T3 Code bugs or missing capabilities. Configure it in **Settings → Labs → Agent feedback**. Reports are scrubbed of file paths, usernames, hostnames, git remotes, and secret-like strings, then stored on this machine only; nothing is sent. Approved cards show **Not sent**. Inspect stored reports with `t3 feedback list [--json]`.

## Agent activity for mobile notifications

**Settings → Sharing & access → Publish agent activity** sends project/thread titles, model names, and turn status to the T3 Connect relay for [mobile notifications and live activities](./mobile-notifications.md). It is off unless you turn it on.

## Export diagnostics to your own OpenTelemetry receiver

Open **Settings → Maintenance → Diagnostics** (per environment) and enter OTLP HTTP endpoints (e.g. `http://localhost:4318/v1/traces`), save, and restart the server. Use **Test** to verify connectivity.

`T3CODE_OTLP_*_URL` and standard `OTEL_EXPORTER_OTLP_*` env vars override saved settings (use `T3CODE_OTLP_HEADERS` / `T3CODE_OTLP_PROTOCOL=http/protobuf` or the standard `OTEL_EXPORTER_OTLP_*` equivalents for auth and protobuf).
