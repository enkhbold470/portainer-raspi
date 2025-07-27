The error "unknown connection 'Wi-Fi connection 1'" happened because your actual Wi-Fi connection name is different. From your output, the active Wi-Fi connection name is **NETGEAR38-5G**.

To set a static IP 192.168.0.100 on this Wi-Fi connection, run these commands with the correct connection name:

```bash
sudo nmcli con mod 'NETGEAR38-5G' ipv4.addresses 192.168.0.100/24
sudo nmcli con mod 'NETGEAR38-5G' ipv4.gateway 192.168.0.1
sudo nmcli con mod 'NETGEAR38-5G' ipv4.dns '8.8.8.8 8.8.4.4'
sudo nmcli con mod 'NETGEAR38-5G' ipv4.method manual
sudo nmcli con down 'NETGEAR38-5G' && sudo nmcli con up 'NETGEAR38-5G'
```

This sets your Wi-Fi to use the specified static IP with your router gateway and DNS servers and applies it by restarting the connection.

If you want to confirm the active connections anytime, you can run:

```bash
nmcli connection show
```

and look for the `NAME` of the Wi-Fi interface with `DEVICE` as `wlan0`.

Let me know if you need help applying these or if you want guidance on any other network setup!

[1] https://askubuntu.com/questions/117065/how-do-i-find-out-the-name-of-the-ssid-im-connected-to-from-the-command-line
[2] https://unix.stackexchange.com/questions/441969/use-nmcli-to-display-the-status-of-a-connection
[3] https://www.reddit.com/r/linuxquestions/comments/1cmp20f/how_do_you_get_network_information_on_linux/
[4] https://serverfault.com/questions/256074/determine-the-wireless-network-name-from-command-line-in-linux
[5] https://stackoverflow.com/questions/60961978/using-perl-to-format-nmcli-output-and-get-wifi-names/60963075
[6] https://manpages.debian.org/bookworm/network-manager/nmcli-examples.7.en.html
[7] https://manpages.debian.org/testing/network-manager/nmcli-examples.7.en.html
[8] https://linux.org/threads/using-nmcli-to-create-wi-fi-connections.54658/
[9] https://people.freedesktop.org/~lkundrak/nm-docs/nmcli-examples.html
[10] https://askubuntu.com/questions/1107627/nmcli-how-to-get-connection-id-or-general-name-of-device
