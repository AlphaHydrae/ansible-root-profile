# Ansible Root Profile

[Ansible](https://www.ansible.com) role that creates a `.profile` file for the root user with the PATH correctly set up for the platform's package manager (e.g. Homebrew or MacPorts).

It also sets the LANG environment variable (to `en_US.UTF-8` by default).



## Role Variables

* `root_profile_lang` - If set, it will be exported as the LANG environment variable (defaults to `en_US.UTF-8`; set to `false` to remove it).
* `root_profile_additional_paths` - Additional semicolon-separated directories to add to the PATH (must end with a semicolon, e.g. `/path1:/path/2:`).
* `root_profile_paths` - Directories that will be added to the PATH (combines `root_profile_additional_paths` and the `host_package_manager_paths` provided by the AlphaHydrae.multipass role).



## Dependencies

The [AlphaHydrae.multipass](https://github.com/AlphaHydrae/ansible-multipass) role is used to determine additional directories to be added to the PATH:

* `host_package_manager_paths` - Additional directories to be added to the PATH for the host's package manager (e.g. `/usr/local/bin:` for Homebrew).



## Example Playbook

    - hosts: servers
      roles:
        - role: AlphaHydrae.root-profile

**With additional directories added to the PATH**

    - hosts: servers
      roles:
        - role: AlphaHydrae.root-profile
          root_profile_additional_paths: "/opt/bin:/usr/bin:"
