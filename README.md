# ha-triones (Forked for Fi Light BLE Lights)

This fork adds support for ONLY Fi Light app based LED BLE lights. If you have any issues please raise and I will try to help you out.
Forked from sysofwan/ha-triones - I have changed the bytes that are sent to the lights to change the colour, and changed how the bytes are read (for status updates on the lights, if a remote is used to change them, it should update in Home Assistant).

<s>Home Assistant integration for BLE based Triones or HappyLighting lights.</s>

Supports controlling BLE based lights controllable through the <s>Triones or HappyLighting</s> Fi Light app<s>s</s>.

## Installation

Note: Restart is always required after installation.

If you want to clone from HACS, either clone this repo and set up as describled below, or clone the original repo (sysofwan/ha-triones) and replace the 'triones.py' file with mine.

This fork should auto-discover any light that advertises with the name "Magic-xxxx..." 

### [HACS](https://hacs.xyz/) (recommended)
Installation can be done through [HACS custom repository](https://hacs.xyz/docs/faq/custom_repositories).

### Manual installation
You can manually clone this repository inside `config/custom_components/triones`.

For  example, from Terminal plugin:
```
cd /config/custom_components
git clone https://github.com/lachiefish/ha-fi-light triones
```

## Setup
After installation, you should find Triones under the Configuration -> Integrations -> Add integration.

The setup step includes discovery which will list out all Triones lights discovered. The setup will validate connection by toggling the selected light. Make sure your light is in-sight to validate this.

The setup needs to be repeated for each light.

## Features
1. Discovery: Automatically discover Triones based lights without manually hunting for Bluetooth MAC address
2. On/Off/RGB/Brightness support
3. Live state polling: External control (i.e. IR remote) state changes will reflect in Home Assistant
4. Emulated RGB brightness: Supports adjusting brightness of RGB lights
5. Multiple light support

## Not supported
[Light modes](https://github.com/madhead/saberlight/blob/master/protocols/Triones/protocol.md#built-in-modes) (blinking, fading, etc) is not yet supported.

## Known issues
1. Light connection may fail a few times after Home Assistant reboot. The integration will usually reconnect and the issue will resolve itself.
2. After toggling lights, Home Assistant may not reflect state changes for up to 30 seconds. This is due to a lag in Triones status API.

## Debugging
Add the following to `configuration.yml` to show debugging logs. Please make sure to include debug logs when filing an issue.

See [logger intergration docs](https://www.home-assistant.io/integrations/logger/) for more information to configure logging.

```yml
logger:
  default: warn
  logs:
    custom_components.triones: debug
```

## Credits
This integration will not be possible without the awesome work of reverse engineering and documenting the Triones BLE protocol [here](https://github.com/madhead/saberlight/blob/master/protocols/Triones/protocol.md).
Forked from sysofwan/ha-triones.
