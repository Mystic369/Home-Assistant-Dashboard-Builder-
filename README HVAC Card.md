# Aprilaire Thermostat Card for Home Assistant

A beautiful custom Lovelace card for Aprilaire thermostats in Home Assistant.

## Installation

### Method 1: Manual Installation

1. Download the `aprilaire-thermostat-card.js` file
2. Copy it to your Home Assistant's `config/www/` directory
3. Add the resource to your Lovelace configuration:
   - Go to **Settings** → **Dashboards** → **Resources** (three dots menu)
   - Click **Add Resource**
   - Set URL to `/local/aprilaire-thermostat-card.js`
   - Set Resource type to **JavaScript Module**
   - Click **Create**

### Method 2: HACS (if available)

If you have HACS installed, you can add this as a custom repository.

## Configuration

Add the card to your Lovelace dashboard:

```yaml
type: custom:aprilaire-thermostat-card
name: Family Room
thermostats:
  - entity: climate.thermostat
outdoor_humidity: sensor.thermostat_outdoor_humidity
weather_entity: weather.home
bottom_buttons:
  - entity: switch.bedroom_fan
    label: BR Fan
  - entity: light.living_room
    label: Living
  - entity: switch.garage_door
    label: Garage
```

## Configuration Options

| Option | Type | Required | Default | Description |
|--------|------|----------|---------|-------------|
| `name` | string | No | `Family Room` | Display name for the card |
| `thermostats` | list | Yes | - | List of thermostat entities |
| `thermostats.entity` | string | Yes | - | Entity ID of your thermostat |
| `outdoor_humidity` | string | No | `sensor.thermostat_outdoor_humidity` | Outdoor humidity sensor |
| `weather_entity` | string | No | `weather.pirateweather` | Weather entity for forecasts |
| `bottom_buttons` | list | No | `[]` | Additional buttons to display at bottom |

## Features

- **Temperature Control**: Adjust heat and cool setpoints independently
- **Mode Switching**: Cycle through heat, cool, heat_cool, and off modes
- **Fan Control**: Switch between auto, on, and circulate fan modes
- **Indoor/Outdoor Display**: Shows current temperature and humidity for both
- **Side Controls**: Dedicated buttons for dehumidifier, air cleaner, and fresh air
- **Custom Bottom Buttons**: Add your own entity controls at the bottom
- **Responsive Design**: Adapts to different screen sizes
- **Visual Feedback**: Animated buttons and status indicators

## Customization

### Bottom Buttons

You can add any Home Assistant entity as a bottom button:

```yaml
bottom_buttons:
  - entity: light.bedroom
    label: Bedroom
  - entity: switch.fan
    label: Fan
  - entity: climate.upstairs
    label: Upstairs
```

### Thermostat Configuration

The card expects your thermostat to have the following attributes:
- `current_temperature`
- `current_humidity`
- `target_temp_low` (for heat setpoint)
- `target_temp_high` (for cool setpoint)
- `fan_mode`
- `hvac_mode` (state)

## Troubleshooting

### Card not appearing
1. Make sure the JavaScript file is in the correct location (`config/www/`)
2. Verify the resource is added in Lovelace resources
3. Clear your browser cache (Ctrl+F5 or Cmd+Shift+R)
4. Check the browser console for errors (F12)

### Entities not updating
1. Verify your entity IDs are correct
2. Check that the entities exist in **Developer Tools** → **States**
3. Make sure your thermostat integration is working properly

### Side controls not working
The dehumidifier, air cleaner, and fresh air buttons have placeholder functions. You'll need to customize these methods in the code to work with your specific entities:

```javascript
toggleDehumidifier() {
  this._hass.callService('switch', 'toggle', {
    entity_id: 'switch.dehumidifier'
  });
}
```

## Support

For issues, questions, or feature requests, please open an issue on GitHub.

## License

MIT License - feel free to modify and use as needed!
