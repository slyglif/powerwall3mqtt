# Changelog

## [0.5.2] - 2025-06-09

### Fixed

- Fix traceback logging related to HTTP ReadTimeouts.

## [0.5.1] - 2025-06-09

### Fixed

- [Issue #45](https://github.com/slyglif/powerwall3mqtt/issues/45): Fix translation for mqtt_username.

## [0.5.0] - 2025-05-23

### Fixed

- [Issue #38](https://github.com/slyglif/powerwall3mqtt/issues/38): Fix translation for mqtt_host on Configuration page.
- [Issue #41](https://github.com/slyglif/powerwall3mqtt/issues/41): Allow polling intervals down to 1 second.

## [0.4.0] - 2025-04-27

### Changes

- Updated README to be more explicit about TeslaPW_XXXXX network requirement.

## [0.3.9] - 2025-04-09

### Changes

- Updated README to note that using the TeslaPW_XXXXX network is required for firmware 25.10.1 or above.

## [0.3.8] - 2025-04-05

### Fixed

- [Issue #36](https://github.com/slyglif/powerwall3mqtt/issues/36): Fix typo from a merge.

## [0.3.2] - 2025-04-05

### Fixed

- [Issue #24](https://github.com/slyglif/powerwall3mqtt/issues/24): Properly handle ConnectTimeout so the log isn't spammed with exceptions.
- [Issue #30](https://github.com/slyglif/powerwall3mqtt/issues/30): Allow anonymous MQTT connections.
- [Issue #33](https://github.com/slyglif/powerwall3mqtt/issues/33): Properly handle ENV boolean options.
- Thanks to @sbman for finding and suggesting fixes for both 30 and 33!

## [0.3.1] - 2025-03-09

### Fixed

- [Issue #23](https://github.com/slyglif/powerwall3mqtt/issues/23): Fix the config entry names for MQTT to line up with the names used by HassIO services.  **NOTE: If you need to use the MQTT hostname or username, you will need up update your config before starting the add-on**

## [0.3.0] - 2025-03-01

### Added

- Added binary_sensors for the following:
	- Backfeed Limited Alert: This is an installer configuration option on the Powerwall that limits export to the grid.  It seems to be used to control operation before permission to operate is granted, and is turned off by Tesla once permission is granted.  If it is enabled after you have permission to operate you should probably reach out to Tesla.
	- Battery Comms Alert: Some kind of communication issue between the system and one of it's batteries.
	- Real Power Config Limited Alert: There was a limit placed on the system during commissioning that prevents generating the amount of power requested.
	- Missing Battery Alert: This is my own alert, based on two sections of the system configuration not matching.  It should mean one or more of the batteries are offline.

## [0.2.0] - 2025-03-01

### Fixed

- [Issue #22](https://github.com/slyglif/powerwall3mqtt/issues/22): Added better error handling of errors fetching individual PW vitals (such as PV string info).  Now the app should log an error and continue running, but mark the individual PWs as unavailable in HA.

### Changed

- This release had a major code cleanup and refactoring, simplifying a lot of the individual functions and classes.  With the exception of the protobuf class, it now passes pylint cleanly using the default settings.  It's possible some edge cases could have issues, so please report any stack traces.  This was preparation for adding unit tests in the future.

## [0.1.3] - 2025-02-27

### Fixed

- [Issue #18](https://github.com/slyglif/powerwall3mqtt/issues/18): Fixed multiple instance of exceptions not being properly handled
- [Issue #19](https://github.com/slyglif/powerwall3mqtt/issues/18): Fixed leaking of passwords into debug logs


## [0.1.2] - 2025-02-26

### Added

- This changelog!
- A loose [roadmap](./ROADMAP.md)

### Fixed

- [Issue #14](https://github.com/slyglif/powerwall3mqtt/issues/14): A better message is logged with a clean exit if unable to connect to PW on startup.
- [Issue #15](https://github.com/slyglif/powerwall3mqtt/issues/15): Fixed handling of throttling so it can properly increase the poll interval.

### Changed

- Converted the git repo to a separate submodule to allow better release tracking

## 0.1.1 - 2025-02-24

### Fixed

- Reverse Battery Power Charge / Discharge calculations
- Fix placement of logging about discovery delay
- Fix the URL for the project


## 0.1.0 - 2025-02-24

### Added

- [Issue #12](https://github.com/slyglif/powerwall3mqtt/issues/12): Import and Export power entities to help support the Energy Dashboard
- Added gradual backoff of loop_interval if throttling is encountered

### Fixed

- [Issue #10](https://github.com/slyglif/powerwall3mqtt/issues/10): Threading shutdown issue that manifested as a hang
- [Issue #2](https://github.com/slyglif/powerwall3mqtt/issues/2): Race condition at startup causing an initial delay in metrics loading in HA
- Check for pw3 on startup


## 0.0.6 - 2025-02-19

### Fixed

- [Issue #1](https://github.com/slyglif/powerwall3mqtt/issues/1): Entities becoming unavailable after an HA restart or reconnect to MQTT


## 0.0.5 - 2025-02-18

### Fixed

- [Issue #9](https://github.com/slyglif/powerwall3mqtt/issues/9): Missing state_class on some entities causes HA warnings


## 0.0.4 - 2025-02-18

### Fixed

- [Issue #8](https://github.com/slyglif/powerwall3mqtt/issues/8): Shutdowns weren't clean, preventing relavent logs from showing

[unreleased]: https://github.com/slyglif/powerwall3mqtt/compare/v0.5.2...HEAD
[0.5.2]: https://github.com/slyglif/powerwall3mqtt/compare/v0.5.1...v0.5.2
[0.5.1]: https://github.com/slyglif/powerwall3mqtt/compare/v0.5.0...v0.5.1
[0.5.0]: https://github.com/slyglif/powerwall3mqtt/compare/v0.4.0...v0.5.0
[0.4.0]: https://github.com/slyglif/powerwall3mqtt/compare/v0.3.9...v0.4.0
[0.3.9]: https://github.com/slyglif/powerwall3mqtt/compare/v0.3.8...v0.3.9
[0.3.8]: https://github.com/slyglif/powerwall3mqtt/compare/v0.3.2...v0.3.8
[0.3.2]: https://github.com/slyglif/powerwall3mqtt/compare/v0.3.1...v0.3.2
[0.3.1]: https://github.com/slyglif/powerwall3mqtt/compare/v0.3.0...v0.3.1
[0.3.0]: https://github.com/slyglif/powerwall3mqtt/compare/v0.2.0...v0.3.0
[0.2.0]: https://github.com/slyglif/powerwall3mqtt/compare/v0.1.3...v0.2.0
[0.1.3]: https://github.com/slyglif/powerwall3mqtt/compare/v0.1.2...v0.1.3
[0.1.2]: https://github.com/slyglif/powerwall3mqtt/compare/v0.1.1...v0.1.2
[0.1.1]: https://github.com/slyglif/powerwall3mqtt/compare/v0.1.0...v0.1.1
[0.1.0]: https://github.com/slyglif/powerwall3mqtt/compare/v0.0.6...v0.1.0
[0.0.6]: https://github.com/slyglif/powerwall3mqtt/compare/v0.0.5...v0.1.6
[0.0.5]: https://github.com/slyglif/powerwall3mqtt/compare/v0.0.4...v0.1.5
[0.0.4]: https://github.com/slyglif/powerwall3mqtt/compare/v0.0.3...v0.1.4
