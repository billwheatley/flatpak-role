# Flatpak Ansible role

Install [Flatpak] applications on Red Hat family, OpenMandriva family or Debian family distributions 

Flatpacks can be found in a variety of sources [flathub](https://flathub.org/) is a common place

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

| name                | description                                                | type | default                                                          |
| ------------------- | ---------------------------------------------------------- | ---- | ---------------------------------------------------------------- |
| flatpak_packages_rh | RPM packages for Red Hat Distributions required by Flatpak | List | [flatpak, flatpak-lib, flatpack-selinux, flatpak-session-helper] |
| flatpak_packages_om | RPM packages for Open Mandriva required by Flatpak         | List | [flatpak]                                                        |

## Example Playbooks

### Using explicitly defined repositories

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
        - name: org.fun.App
          remote: customRepo
      flatpak_repos:
        - name: flathub
          url: https://flathub.org/repo/flathub.flatpakrepo
        - name: customRepo
          url: https://mycustomrepo.org/repo/flathub.flatpakrepo
```

### Using the default repository

```yaml
- hosts: workstations
  tasks:
  - import_role:
      name: flatpack
    vars:
      flatpak_apps:
        - name: com.slack.Slack
        - name: com.spotify.Client
        - name: org.videolan.VLC
```

## License

[MIT](LICENSE)

[flatpak]: https://flatpak.org/
