# Critical Sensor Notification Manager

A Home Assistant automation blueprint for critical binary sensors such as water-leak, smoke, freezer, sump-pump, and other safety sensors.

## Features

- Select one or more `binary_sensor` entities.
- Each active sensor is tracked independently with parallel automation runs.
- Sends an immediate actionable notification.
- Supports iOS critical notification sound.
- Provides a unique **Acknowledge Alert** action for each alert run.
- Sends configurable reminders (default: 5 and 10 minutes).
- Stops reminders when the alert is acknowledged.
- Detects recovery when the triggering sensor returns to `off`.
- Optionally creates a persistent Home Assistant notification while the condition is active.
- Sends a recovery notification when the condition clears.
- Uses the sensor's Home Assistant Area as its location when available, otherwise the entity name.
- No helper entities are required.
- Multiple sensors can be active simultaneously without sharing an acknowledgement state.

## Installation

### Import from GitHub

1. Open **Settings → Automations & scenes → Blueprints** in Home Assistant.
2. Select **Import Blueprint**.
3. Enter the URL to this blueprint file:

   `https://raw.githubusercontent.com/rng-coder/Critical-Sensor-Notification-Manager-Blueprint/main/blueprints/automation/rng-coder/critical_sensor_notification_manager.yaml`

4. Import the blueprint.
5. Create an automation from **Critical Sensor Notification Manager**.

### Manual installation

Copy the YAML file into:

```text
config/blueprints/automation/rng-coder/critical_sensor_notification_manager.yaml
```

Then reload Automations or restart Home Assistant if necessary.

## Recommended configuration

For a water-leak installation:

- **Critical sensors:** select all leak sensors.
- **Notification recipients:** select your Mobile App notify entity/entities.
- **Reminder interval:** `5` minutes.
- **Reminder count:** `2`.
- **Critical sound:** enabled.
- **Persistent Home Assistant alert:** enabled.

This produces an initial alert, a reminder at approximately 5 minutes, and another at approximately 10 minutes. The automation then watches for acknowledgement or recovery for one final interval before ending the run.

## Important: iOS notifications

For actionable iPhone notifications and critical sound, use the Home Assistant Companion App Mobile App notification entity. iOS may require expanding or press-and-holding the notification before the custom **ACKNOWLEDGE ALERT** action is visible.

Critical alerts also depend on the iOS/Home Assistant notification permission settings allowing critical alerts.

## How alert runs work

Each sensor activation creates its own parallel automation run. The run has a unique acknowledgement action ID, so acknowledging one sensor does not acknowledge another sensor that is currently active.

The persistent notification ID is also derived from the triggering entity, preventing simultaneous sensors from overwriting each other's Home Assistant persistent alert.

## Repository security

This repository is public and intentionally contains reusable blueprint code only. It must never contain a Home Assistant backup, `secrets.yaml`, `.storage/` data, passwords, access tokens, API keys, or private personal configuration.

The repository includes:

- `.gitignore` rules for Home Assistant runtime data, secrets, backups, and common local files.
- `SECURITY.md` with private vulnerability-reporting guidance.
- `.github/CODEOWNERS` assigning repository ownership to `@rng-coder`.
- An MIT `LICENSE`.

GitHub **secret scanning**, **push protection**, and **code scanning** should remain enabled. For stronger `main`-branch protection, configure a GitHub ruleset requiring pull requests and, once useful CI checks exist, successful status checks before merging. GitHub supports requiring code-owner review as part of branch protection. 

## Validation status

The blueprint has been reviewed against the current Home Assistant blueprint, selector, notification, and wait-for-trigger syntax. It is designed for Home Assistant 2026.9 or newer.

The final validation step is importing the blueprint into a real Home Assistant instance and testing the notification behavior. Recommended test order:

1. One test binary sensor.
2. Initial notification and critical sound.
3. Acknowledge action.
4. Five- and ten-minute reminders.
5. Sensor recovery.
6. Two sensors active simultaneously.

## License

MIT
