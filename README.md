Ansible Role: dovecot(src)
================================================================================
Build and insall dovecot from a source code into /opt/dovecot.

* Build and install dovecot 2.2 into /opt/dovecot
* Deploy files into /opt/dovecot/etc
* Open tcp/110, tcp/143, tcp/993, and tcp/995.

Requirements
--------------------------------------------------------------------------------
None.

Role Variables
--------------------------------------------------------------------------------
The following variables are defined in defaults/main.yml file.

```yaml
dovecot:
  started: true
  enabled: true
  rebuild: false
  version: "2.2.29"
  majorver: "2.2"
  updateonly: false
  initscript: "dovecot"
  serverroot: "/opt/dovecot"
  workingdir: "/usr/local/src"
  user:
    daemon:
      username: "dovecot"
      group: "dovecot"
      uid: "715"
      gid: "715"
      home: "/opt/dovecot/var"
      shell: "/sbin/nologin"
      comment: '"Dovecot Daemon"'
    login:
      username: "dovenull"
      group: "dovecot"
      uid: "716"
      gid: "715"
      home: "/opt/dovecot/var"
      shell: "/sbin/nologin"
      comment: '"Dovecot Login"'
    mailbox:
      # Values should be same as the following roles
      # - sendmail.user.mda
      # - opensmtpd.user.mailbox
      username: "virtmail"
      group: "virtmail"
      uid: "660"
      gid: "660"
      home: "/home/virtmail"
      shell: "/bin/sh"
      comment: "'Virtual Mailbox'"
  config:
    certificate:
      country: "JP"
      state: "Kyoto"
      city: "Kyoto"
      organization: "Nyaan"
      section: "'Mail Server'"
      commonname: "mail.{{ ansible_domain }}"
      email: "postmaster@{{ ansible_domain }}"
  packages:
    freebsd:
      install: ["db48"]
    redhat:
      install: ["db4", "db4-devel"]
procmail:
  rebuild: false
  version: "3.22"
  install: "/usr/local"
  spool: "/var/spool/procmail"
maildrop:
  rebuild: false
  version: "2.7.2"
  install: "/usr/local"
```

Dependencies
--------------------------------------------------------------------------------
None. 

Example Playbook
--------------------------------------------------------------------------------
```yaml
- hosts: servers
  roles:
     - { role: azumakuniyuki.ar-dovecot-src }
```

License
--------------------------------------------------------------------------------
BSD

Author Information
--------------------------------------------------------------------------------
[azumakuniyuki](http://nyaan.jp/)
