# Build

- `makepkg -s` to build. Add `-f` if you're testing and want to rebuild.
- `makepkg -si` to install.

# Start

1. REBOOT your system! Just in case you did a kernel update!

```sh
# Start the PanGPS server daemon
sudo systemctl start --enable gpd
# Start the PanGPA client agent
systemctl --user --enable start gpa

# Now you can either directly open the GUI via
PanGPUI
# or
globalprotect launch-ui

# Or you can interact with the setup via the interactive prompt
globalprotect
```

# Troubleshooting

- Error "Cannot parse your input. The valid CLI commands that you can now use are:".
  The GUI is running, you can't use the CLI simultaneously. Kill the GUI first.
- Check if the PanGPS is crashing (`sudo systemctl status gpd.service`).
  If so, the string "s/\x55\x62\x75\x6e\x74\x75/\x41\x72\x63\x68\x20\x4c/g" might not be correctly replaced
- Check if PanGPS is opening a port on `4767`. This is required for the `PanGPA` agent to connect.
- No internet after vpn stop/restart: `sudo systemctl restart systemd-resolved`
  `globalprotect` replaces resolved with something custom.
  When globalprotect is not properly shut down, resolved might not recover.
- If stuff is still fucked: Try to reboot
