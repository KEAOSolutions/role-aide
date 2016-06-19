centisible.role-aide
=========

This role ensures `AIDE` package is installed and configured.


Requirements
------------

None.


Role Variables
--------------

The following variables are defined
* `aide_packages_list: [ 'aide' ]`
* `aide_packages_state: 'present'`
* `aide_packages_disable_gpg_check: 'no'`
* `aide_packages_update_cache: 'yes'`
* `aide_packages_validate_certs: 'yes'`
* `aide_config_file_mode: '0400'`
* `aide_config_file_owner: 'root'`
* `aide_config_file_group: 'root'`
* `aide_config_file_dest: '/etc/aide.conf'`
* `aide_config_file_src: 'etc/aide.conf.j2'`
* `aide_config_file_backup: true`
* `aide_config_file_validate: 'aide -c %s -D'`


aide_config_verbosity: '5'

* `aide_config_database: 'file:{{ aide_config_db_path }}'`
* `aide_config_database_out: 'file:{{ aide_config_db_new_path }}'`
* `aide_config_report_url: 'file:@@{LOGDIR}/aide.log'`
* `aide_config_gzip_out: 'yes'`
* `aide_config_dir_log_path: '/var/log/aide'`
* `aide_config_dir_log_owner: 'root'`
* `aide_config_dir_log_group: 'root'`
* `aide_config_dir_log_mode: '0700'`
* `aide_config_dir_log_state: 'directory'`
* `aide_config_dir_db_path: '/var/lib/aide'`
* `aide_config_dir_db_owner: 'root'`
* `aide_config_dir_db_group: 'root'`
* `aide_config_dir_db_mode: '0700'`
* `aide_config_dir_db_state: 'directory'`
* `aide_config_db_path: '{{ aide_config_dir_db_path }}/aide.db.gz'`
* `aide_config_db_owner: 'root'`
* `aide_config_db_group: 'root'`
* `aide_config_db_mode: '0600'`
* `aide_config_db_state: 'file'`
* `aide_config_db_new_path: '{{ aide_config_dir_db_path }}/aide.db.new.gz'`
* `aide_config_db_new_owner: 'root'`
* `aide_config_db_new_group: 'root'`
* `aide_config_db_new_mode: '0600'`
* `aide_config_db_new_state: 'absent'

```
aide_config_definitions:
  - { name: 'LOGDIR',  desc: '{{ aide_config_dir_log_path }}' }
```

```
aide_config_rules:
  - { name: 'FIPSR',          desc: 'p+i+n+u+g+s+m+c+acl+selinux+xattrs+sha256'}
  - { name: 'ALLXTRAHASHES',  desc: 'sha1+rmd160+sha256+sha512+tiger' }
  - { name: 'NORMAL',         desc: 'FIPSR+sha512' }
  - { name: 'DIR',            desc: 'p+i+n+u+g+acl+selinux+xattrs' }
  - { name: 'PERMS',          desc: 'p+i+u+g+acl+selinux' }
  - { name: 'LOG',            desc: '>' }
  - { name: 'LSPP',           desc: 'FIPSR+sha512' }
  - { name: 'DATAONLY',       desc: 'p+n+u+g+s+acl+selinux+xattrs+sha256' }
```

```
aide_config_content:
  - { path: '/boot',                     desc: 'NORMAL' }
  - { path: '/bin',                      desc: 'NORMAL' }
  - { path: '/sbin',                     desc: 'NORMAL' }
  - { path: '/lib',                      desc: 'NORMAL' }
  - { path: '/lib64',                    desc: 'NORMAL' }
  - { path: '/opt',                      desc: 'NORMAL' }
  - { path: '/usr',                      desc: 'NORMAL' }
  - { path: '/root',                     desc: 'NORMAL' }
  - { path: '/etc',                      desc: 'PERMS' }
  - { path: '/etc/exports',              desc: 'NORMAL' }
  - { path: '/etc/fstab',                desc: 'NORMAL' }
  - { path: '/etc/passwd',               desc: 'NORMAL' }
  - { path: '/etc/group',                desc: 'NORMAL' }
  - { path: '/etc/gshadow',              desc: 'NORMAL' }
  - { path: '/etc/shadow',               desc: 'NORMAL' }
  - { path: '/etc/security/opasswd',     desc: 'NORMAL' }
  - { path: '/etc/hosts.allow',          desc: 'NORMAL' }
  - { path: '/etc/hosts.deny',           desc: 'NORMAL' }
  - { path: '/etc/sudoers',              desc: 'NORMAL' }
  - { path: '/etc/skel',                 desc: 'NORMAL' }
  - { path: '/etc/logrotate.d',          desc: 'NORMAL' }
  - { path: '/etc/resolv.conf',          desc: 'DATAONLY' }
  - { path: '/etc/nscd.conf',            desc: 'NORMAL' }
  - { path: '/etc/securetty',            desc: 'NORMAL' }
  - { path: '/etc/profile',              desc: 'NORMAL' }
  - { path: '/etc/bashrc',               desc: 'NORMAL' }
  - { path: '/etc/bash_completion.d/',   desc: 'NORMAL' }
  - { path: '/etc/login.defs',           desc: 'NORMAL' }
  - { path: '/etc/zprofile',             desc: 'NORMAL' }
  - { path: '/etc/zshrc',                desc: 'NORMAL' }
  - { path: '/etc/zlogin',               desc: 'NORMAL' }
  - { path: '/etc/zlogout',              desc: 'NORMAL' }
  - { path: '/etc/profile.d/',           desc: 'NORMAL' }
  - { path: '/etc/X11/',                 desc: 'NORMAL' }
  - { path: '/etc/yum.conf',             desc: 'NORMAL' }
  - { path: '/etc/yumex.conf',           desc: 'NORMAL' }
  - { path: '/etc/yumex.profiles.conf',  desc: 'NORMAL' }
  - { path: '/etc/yum/',                 desc: 'NORMAL' }
  - { path: '/etc/yum.repos.d/',         desc: 'NORMAL' }
  - { path: '/var/log',                  desc: 'LOG' }
  - { path: '/var/run/utmp',             desc: 'LOG' }
  - { path: '/etc/audit/',               desc: 'LSPP' }
  - { path: '/etc/libaudit.conf',        desc: 'LSPP' }
  - { path: '/usr/sbin/stunnel',         desc: 'LSPP' }
  - { path: '/var/spool/at',             desc: 'LSPP' }
  - { path: '/etc/at.allow',             desc: 'LSPP' }
  - { path: '/etc/at.deny',              desc: 'LSPP' }
  - { path: '/etc/cron.allow',           desc: 'LSPP' }
  - { path: '/etc/cron.deny',            desc: 'LSPP' }
  - { path: '/etc/cron.d/',              desc: 'LSPP' }
  - { path: '/etc/cron.daily/',          desc: 'LSPP' }
  - { path: '/etc/cron.hourly/',         desc: 'LSPP' }
  - { path: '/etc/cron.monthly/',        desc: 'LSPP' }
  - { path: '/etc/cron.weekly/',         desc: 'LSPP' }
  - { path: '/etc/crontab',              desc: 'LSPP' }
  - { path: '/var/spool/cron/root',      desc: 'LSPP' }
  - { path: '/etc/login.defs',           desc: 'LSPP' }
  - { path: '/etc/securetty',            desc: 'LSPP' }
  - { path: '/var/log/faillog',          desc: 'LSPP' }
  - { path: '/var/log/lastlog',          desc: 'LSPP' }
  - { path: '/etc/hosts',                desc: 'LSPP' }
  - { path: '/etc/sysconfig',            desc: 'LSPP' }
  - { path: '/etc/inittab',              desc: 'LSPP' }
  - { path: '/etc/grub/',                desc: 'LSPP' }
  - { path: '/etc/rc.d',                 desc: 'LSPP' }
  - { path: '/etc/ld.so.conf',           desc: 'LSPP' }
  - { path: '/etc/localtime',            desc: 'LSPP' }
  - { path: '/etc/sysctl.conf',          desc: 'LSPP' }
  - { path: '/etc/modprobe.conf',        desc: 'LSPP' }
  - { path: '/etc/pam.d',                desc: 'LSPP' }
  - { path: '/etc/security',             desc: 'LSPP' }
  - { path: '/etc/aliases',              desc: 'LSPP' }
  - { path: '/etc/postfix',              desc: 'LSPP' }
  - { path: '/etc/ssh/sshd_config',      desc: 'LSPP' }
  - { path: '/etc/ssh/ssh_config',       desc: 'LSPP' }
  - { path: '/etc/stunnel',              desc: 'LSPP' }
  - { path: '/etc/vsftpd.ftpusers',      desc: 'LSPP' }
  - { path: '/etc/vsftpd',               desc: 'LSPP' }
  - { path: '/etc/issue',                desc: 'LSPP' }
```

```
aide_run_init_db:
  - 'aide --init'
  - 'mv -v {{ aide_config_db_new_path }} {{ aide_config_db_path }}'
```


Dependencies
------------

None.


Example Playbook
----------------

```
    - hosts: all
      roles:
         - centisible.role-aide
```


License
-------

GPLv3


Author Information
------------------

Kamil Boratyński <kamil.boratynski@icloud.com>
