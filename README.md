# Flatpak

Install [Flatpak][flatpak] applications on Fedora.

## Role Variables

### defaults/main.yml

| name          | description                       | type | default   |
| ------------- | --------------------------------- | ---- | --------- |
| flatpak_apps  | Installed Flatpak applications    | List | []        |
| flatpak_repos | Added Flatpak remote repositories | List | [flathub] |

#### Example Usage

```yaml
flatpak_apps:
  - name: org.videolan.VLC
    remote: flathub
```

```yaml
flatpak_repos:
  - name: flathub
    url: https://flathub.org/repo/flathub.flatpakrep
```

### vars/main.yml

| name             | description                      | type | default                                                          |
| ---------------- | -------------------------------- | ---- | ---------------------------------------------------------------- |
| flatpak_packages | RPM packages required by Flatpak | List | [flatpak, flatpak-lib, flatpack-selinux, flatpak-session-helper] |

## Example Playbook

```yaml
- hosts: workstations
  tasks:
  - import_role:
      name: flatpack
    vars:
      flatpak_apps:
        - name: com.slack.Slack
          remote: flathub
        - name: com.spotify.Client
          remote: flathub
        - name: org.videolan.VLC
          remote: flathub
      flatpak_repos:
        - name: flathub
          url: https://flathub.org/repo/flathub.flatpakrepo
```

## License

[MIT](LICENSE)

[flatpak]: https://flatpak.org/
