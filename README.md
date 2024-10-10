
# Ansible role: File Copy, Messaging, OS Information, and Host Management

## Overview

This Ansible role performs the following tasks on remote hosts:
1. Copy a file from the control node to the host.
2. Print a message three times, with a variable changing in each iteration.
3. Display the OS family of the remote host.
4. Set and display a custom variable.
5. Manage logs on the control node (master).
6. Reboot the remote host and log the reboot time.

## Tasks Breakdown

### 1. **Copy File to Hosts**
```yaml
- name: Copy file 1.txt to host
  copy:
    src: files/1.txt
    dest: /home/1.txt
```
This task copies `1.txt` from the `files` directory on the control node to the `/home/` directory on the remote host.

### 2. **Print a Message 3 Times with Changing Variable**
```yaml
- name: Print message three times using a loop
  debug:
    msg: "This is message {{ item }}"
  loop:
    - "dima"
    - "give me pls"
    - "100"
```
This task prints a message three times, with the content of the message changing based on the loop variable.

### 3. **Print the OS Family of the Host**
```yaml
- name: Print os_family of host
  debug:
    msg: "OS family of the host is {{ ansible_os_family }}"
```
This task prints the OS family (e.g., `Debian`, `RedHat`) of the remote host.

### 4. **Set and Print a Variable**
```yaml
- name: Set variable
  set_fact:
    my_variable: "dima ty for 100"

- name: Print variable
  debug:
    msg: "{{ my_variable }}"
```
This task sets a custom variable and then prints it.

### 5. **Ensure Log Directory Exists**
```yaml
- name: Ensure log directory exists
  delegate_to: localhost
  file:
    path: /files
    state: directory
```
This task ensures that the `/files` directory exists on the control node.

### 6. **Save Host IP in `log.txt` on the Master**
```yaml
- name: Save host IP in log.txt on master
  delegate_to: localhost
  shell: echo "{{ ansible_host }}" >> /files/log.txt
```
This task appends the IP address of the remote host to `log.txt` on the control node.

### 7. **Reboot the Host**
```yaml
- name: Reboot host
  delegate_to: "{{ inventory_hostname }}"
  reboot:
```
This task reboots the remote host.

### 8. **Log Reboot Time in `log.txt`**
```yaml
- name: Save reboot time in log.txt
  delegate_to: localhost
  shell: "echo 'Host {{ inventory_hostname }} rebooted at $(date -Ins)' >> /files/log.txt"
```
This task appends the reboot time of the host to `log.txt` on the control node.

## How to Run

1. **Playbook Setup**: Ensure the playbook is correctly structured, with the necessary files in place (e.g., `files/1.txt`).
2. **Define Inventory**: Make sure your inventory file has the target hosts defined.
3. **Execute the Playbook**: Run the playbook using:
   ```bash
   ansible-playbook -i inventory my_playbook.yml
   ```

## Notes

- Ensure the file `1.txt` exists in the `files` directory on the control node.
- The logs will be saved to `/files/log.txt` on the control node (master).
- Make sure the user running the playbook has the necessary permissions to reboot the hosts.

---

This playbook is part of my DevOps studies, demonstrating tasks like file copying, dynamic messaging, gathering OS information, and managing host reboots with logging.
