# macOS

[macOS](https://www.apple.com/macos) (previously Mac OS X and later OS X) is a proprietary graphical operating system developed and marketed by Apple Inc. since 2001.

## FileVault

### Validate key

```shell
sudo fdesetup validaterecovery
```

## iCloud Drive

### Create [iCloud Drive](https://support.apple.com/en-us/HT201104) symbolic link to Home

```shell
ln -s "/Users/$USER/Library/Mobile Documents/com~apple~CloudDocs" iCloud
```

## Security & Privacy

### System Integrity Protection Temporarily

> <https://developer.apple.com/documentation/security/disabling_and_enabling_system_integrity_protection>

#### Disable System Integrity Protection Temporarily

To disable SIP, do the following:

1. Restart your computer in Recovery mode.
2. Launch Terminal from the Utilities menu.
3. Run the command `csrutil disable`.
4. Restart your computer.

#### Enable System Integrity Protection

To reenable SIP, do the following:

1. Restart your computer in Recovery mode.
2. Launch Terminal from the Utilities menu.
3. Run the command `csrutil enable`.
4. Restart your computer.

### Reset and Remove Applications in Location Services

1. Start terminal and then sudo to a root shell

    ```shell
    sudo -s
    ```

2. Go to `/var/db/locationd`

    ```shell
    cd /var/db/locationd
    ```

3. Convert clients.plist to xml (editable format)

    ```shell
    plutil -convert xml1 clients.plist
    ```

4. Edit the clients.plist file and remove the application. Convert the `clients.plist` file back to binary

    ```shell
    plutil -convert binary1 clients.plist
    ```

5. Restart `locationd`

    ```shell
    killall locationd
    ```

## Time Machine

### Delete Time Machine local snapshots

```shell
for snapshot in $(tmutil listlocalsnapshotdates | grep -v :); do sudo tmutil deletelocalsnapshots $snapshot; done
```
