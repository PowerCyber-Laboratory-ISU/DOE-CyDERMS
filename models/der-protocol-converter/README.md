# DER Protocol Converter

This folder contains the DER Protocol Converter model components used by the CyDERMS project. The converter supports protocol translation between SunSpec Modbus-based DER devices and DNP3-based utility or DERMS systems.

The components are included as Git submodules so each software package can remain versioned and maintained in its own repository while being referenced from the main `DOE-CyDERMS` project repository.

## Components

| Folder | Role | Description |
| --- | --- | --- |
| `der-gateway-client/` | SunSpec Modbus Client | Python client that connects to SunSpec-certified DER devices or servers over Modbus TCP. It monitors DER measurements and executes DER management commands. |
| `dnp3-rust-resources/` | DNP3 Outstation | Rust-based DNP3 endpoint representing DER devices to upstream utility, SCADA, or DERMS systems. It exposes monitoring data and receives control commands. |
| `sunspec-modbus-server-v1/` | SunSpec Modbus Server | Python-based SunSpec Modbus TCP server that simulates a DER device for testing and experimentation. |

## Architecture Overview

The DER Protocol Converter links a SunSpec Modbus endpoint with a DNP3 outstation endpoint using shared JSON exchange files.

```text
DER device or simulator
        |
        | SunSpec Modbus TCP
        v
der-gateway-client
        |
        | DERMeasurement.json / DERManagement.json
        v
dnp3-rust-resources
        |
        | DNP3 TCP
        v
Utility SCADA / DERMS / DNP3 master
```

The SunSpec Modbus server can be used as a local test DER device when physical DER hardware is not available.

## Data Exchange

The converter uses two JSON files for information exchange between the Modbus-side client and the DNP3-side outstation:

- `DERMeasurement.json` - DER telemetry and monitoring data flowing from Modbus to DNP3.
- `DERManagement.json` - DER management and control commands flowing from DNP3 to Modbus.

## Typical Use

1. Start `sunspec-modbus-server-v1` if a simulated DER device is needed.
2. Configure and run `der-gateway-client` to connect to the SunSpec Modbus device or simulator.
3. Configure and run `dnp3-rust-resources` to expose DER data through DNP3.
4. Connect a DNP3 master, SCADA tool, or DERMS test environment to the DNP3 outstation.

Each submodule includes its own README with installation, configuration, and execution details.

## Cloning This Repository With Submodules

Use this command when cloning `DOE-CyDERMS` so the submodule contents are downloaded automatically:

```bash
git clone --recurse-submodules https://github.com/PowerCyber-Laboratory-ISU/DOE-CyDERMS.git
```

If the repository has already been cloned, initialize and update submodules with:

```bash
git submodule update --init --recursive
```

## Updating Submodules

To update the submodules to newer commits from their respective repositories:

```bash
git submodule update --remote --merge
```

After reviewing the updates, commit the changed submodule references in the main `DOE-CyDERMS` repository.

## Notes

- The submodules are maintained as separate repositories under the `PowerCyber-Laboratory-ISU` GitHub organization.
- Do not delete the forked repositories unless the submodules are replaced with regular copied files.
- The individual components are designed for Linux-based environments.