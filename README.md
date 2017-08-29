# Ansible Role: rsync

## info
rsync是类unix系统下的数据镜像备份工具——remote sync。一款快速增量备份工具 Remote Sync，远程同步 支持本地复制，或者与其他SSH、rsync主机同步。

官方地址： http://rsync.samba.org/
官方文档地址：http://rsync.samba.org/documentation.html

## os env

ansible `2.x`
os `ubuntu 14.04`

## var
	xinetd_ip: "{{ ansible_default_ipv4.address }}" #"{{ ansible_eth0.ipv4.address }}"

    rsync_user: "root"
    rsync_group: "root"
    rsync_conf: "/etc/rsyncd.conf"

    rsync_authusers: [] # ["test:123456"]
    rsync_passfile: "/etc/rsyncd.password"

    rsync_port: 873
    rsync_maxconn: 200
    rsync_timeout: 300
    rsync_chroot: no
    rsync_shares: {} #{"name": "test", "path": "/data"}

## require
xinetd

## Example Playbook

	---
    - name: Test the plabybook API.
      hosts: all
      remote_user: root
      gather_facts: yes
      roles:
        - role: ansible-rsync
          rsync_authusers: ["nobody:123456"]
          xinetd_ip: "{{ ansible_eth0.ipv4.address }}"
          rsync_shares:
            - name : stock
              "path": "/data/LOneClient/data"
              "comment": "stock"
              "authuser": "nobody"
		    - name: data2
			  comment: Public data2
			  path: /data/2