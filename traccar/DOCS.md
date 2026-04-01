# Home Assistant Add-on: Traccar

[Traccar][traccar] is a modern GPS Tracking Platform, available as a Home
Assistant add-on. Run your GPS tracking server without any cloud dependency.

Traccar supports more protocols and device models than any other GPS tracking
system on the market. You can select GPS trackers from low-cost Chinese models
to high-end quality brands.

## Installation

1. Install the official **MariaDB** add-on and ensure it is running.
2. Add this repository to Home Assistant:
   **Settings → Add-ons → Add-on Store → ⋮ → Repositories**
3. Find **Traccar** and click **Install**.
4. Start the add-on and check the logs.
5. Click **OPEN WEB UI**.

Default credentials: `admin` / `admin` — change immediately after first login.

## Configuration

```yaml
log_level: info
ssl: false
certfile: fullchain.pem
keyfile: privkey.pem
```

### Option: `log_level`

Controls log verbosity. Options: `trace`, `debug`, `info`, `notice`,
`warning`, `error`, `fatal`.

### Option: `ssl`

Enables HTTPS on the web interface. Set to `true` to enable.

### Option: `certfile`

SSL certificate file (must be in `/ssl/`).

### Option: `keyfile`

SSL private key file (must be in `/ssl/`).

## Enabling GPS protocols

By default only the OsmAnd protocol (port 5055) is enabled.
To activate more protocols, edit `/addon_configs/traccar/traccar.xml`:

```xml
<entry key='gt06.port'>5023</entry>
<entry key='teltonika.port'>5027</entry>
```

Full list: <https://www.traccar.org/devices/>

## Home Assistant integration

Add to `configuration.yaml`:

```yaml
device_tracker:
  - platform: traccar
    host: localhost
    port: 18682
    username: YOUR_EMAIL
    password: YOUR_PASSWORD
```

Or use the **Traccar Server** integration via UI:
**Settings → Integrations → Add → Traccar Server**

## Database

Without MariaDB add-on the server uses the internal H2 database (not
recommended for production). With MariaDB running, the add-on automatically
creates the `traccar` database and configures the connection.

[traccar]: https://www.traccar.org
