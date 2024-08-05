### README.md

```markdown
# Background Process Manager

This repository contains a Python script that manages running an executable (either a Python script or a binary executable) at specified intervals in the background. It also includes an Ansible playbook to manage the background process on a Windows machine.

## Features

- Start an executable at a specified interval in the background.
- Stop the background process.
- Check the status of the background process.
- Designed to work on Windows 10.
- Ansible playbook for managing the process.

## Requirements

- Python 3.x
- Ansible (for remote management via playbook)
- Windows 10 (for running the script and Ansible playbook)

## Usage

### Script

#### Start the Background Process

```sh
python process_manager.py start --interval <INTERVAL_IN_SECONDS> --executable-path <PATH_TO_EXECUTABLE> --pid-file <PATH_TO_PID_FILE>
```

Example:
```sh
python process_manager.py start --interval 60 --executable-path C:\path\to\your_script.py --pid-file C:\path\to\process.pid
```

#### Stop the Background Process

```sh
python process_manager.py stop --pid-file <PATH_TO_PID_FILE>
```

Example:
```sh
python process_manager.py stop --pid-file C:\path\to\process.pid
```

#### Check the Status of the Background Process

```sh
python process_manager.py status --pid-file <PATH_TO_PID_FILE>
```

Example:
```sh
python process_manager.py status --pid-file C:\path\to\process.pid
```

### Ansible Playbook

#### Playbook Structure

```yaml
---
- name: Manage executable background process on Windows
  hosts: windows
  tasks:
    - name: Start the executable background process
      win_shell: |
        python C:\path\to\process_manager.py start --interval 60 --executable-path C:\path\to\executable.exe --pid-file C:\path\to\process.pid
      args:
        executable: cmd
      when: action == "start"

    - name: Stop the executable background process
      win_shell: |
        python C:\path\to\process_manager.py stop --pid-file C:\path\to\process.pid
      args:
        executable: cmd
      when: action == "stop"

    - name: Check the status of the executable background process
      win_shell: |
        python C:\path\to\process_manager.py status --pid-file C:\path\to\process.pid
      args:
        executable: cmd
      when: action == "status"

  vars:
    action: "{{ action }}"
```

#### Running the Playbook

To run the playbook, specify the action variable to start, stop, or check the status of the background process.

##### Start the Background Process

```sh
ansible-playbook manage_process.yml -e "action=start"
```

##### Stop the Background Process

```sh
ansible-playbook manage_process.yml -e "action=stop"
```

##### Check the Status of the Background Process

```sh
ansible-playbook manage_process.yml -e "action=status"
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

Please feel free to submit issues, fork the repository and send pull requests!

## Author

- [MrSud0](https://github.com/MrSud0)
