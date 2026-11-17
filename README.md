# Orca Filament Profiles

Choose which OrcaSlicer preset **Filament & Color** sync uses for each AFC
material label. For example, map plain `PLA` on your Creator 5 Pro to
**Flashforge PLA Color Change**.

This plugin requires OrcaSlicer 2.5 or later and an OpenCreator AFC build that
publishes Moonraker lane data. It adds `filament_id` when a lane has a matching
material label and AFC has supplied no ID. A preset ID from AFC takes
precedence.

## Install

Connect to the OpenCreator host over SSH and run:

```sh
oc-plugin install --no-restart https://github.com/Xmister/opencreator-orca-filament-profiles
```

In the directory that contains `printer.cfg`, create a folder named
`orca-filament-profiles` and save your mappings in it as `mapping.cfg`. The
following example uses stock OrcaSlicer 2.5 presets for the Flashforge
Creator 5 Pro:

```ini
[oc_orca_filament_profiles]
filament_ids:
    PLA: OFMkAW6r
    PETG: OFXiArjA
    TPU-90A: OFwlZ7gH
```

Use material labels that AFC publishes, and the `filament_id` from a compatible
preset in your OrcaSlicer version. Each mapping applies to every lane carrying
that material label. Case, spaces, hyphens, and underscores are normalized, so
`TPU-90A` and `tpu_90a` match the same entry. An empty mapping leaves Orca's
normal selection in place.

Restart Klipper while the printer is idle. In OrcaSlicer, run
**Synchronize filament list from AMS** with **Filament & Color** selected.
To inspect what Orca receives, open
`http://<printer-ip>:7125/server/database/item?namespace=lane_data`.

The mapping lives alongside your printer configuration, outside both the
plugin and Kalico Git checkouts. Update the plugin with
`oc-plugin update orca-filament-profiles`. Use
`oc-plugin disable orca-filament-profiles` to return to normal AFC publishing.
