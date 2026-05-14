# Service Management

Linux services are managed using `systemd`.

## Check Service Status

```bash
systemctl status <service>
```

## Start a Service

```bash
sudo systemctl start <service>
```

## Stop a Service

```bash
sudo systemctl stop <service>
```

## Restart a Service

```bash
sudo systemctl restart <service>
```

## Enable a Service at Boot

```bash
sudo systemctl enable <service>
```