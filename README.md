# Ansibleテスト

## 参考サイト

- https://qiita.com/Shoma0210/items/7d7d24d7c3f95f19b427
- https://qiita.com/cheekykorkind/items/e6f39c47c503c1b36924

## 実行方法

```bash
docker compose up -d
```

## 動作確認

Ansibleの動作確認

```bash
$ docker compose exec ansible ansible localhost -m ping

localhost | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

```bash
$ docker compose exec ansible ansible -i hosts -m ping all

[WARNING]: Platform linux on host node03 is using the discovered Python interpreter at /usr/bin/python3.9, but future installation of
another Python interpreter could change the meaning of that path. See https://docs.ansible.com/ansible-
core/2.15/reference_appendices/interpreter_discovery.html for more information.
node03 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.9"
    },
    "changed": false,
    "ping": "pong"
}
[WARNING]: Platform linux on host node02 is using the discovered Python interpreter at /usr/bin/python3.9, but future installation of
another Python interpreter could change the meaning of that path. See https://docs.ansible.com/ansible-
core/2.15/reference_appendices/interpreter_discovery.html for more information.
node02 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.9"
    },
    "changed": false,
    "ping": "pong"
}
[WARNING]: Platform linux on host node01 is using the discovered Python interpreter at /usr/bin/python3.9, but future installation of
another Python interpreter could change the meaning of that path. See https://docs.ansible.com/ansible-
core/2.15/reference_appendices/interpreter_discovery.html for more information.
node01 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.9"
    },
    "changed": false,
    "ping": "pong"
}
```

## Playbookの実行

```bash
$ docker compose exec ansible ansible-playbook playbook.yml

PLAY [deploy httpd server] ***********************************************************************************************************

TASK [install httpd] *****************************************************************************************************************
[WARNING]: Platform linux on host node02 is using the discovered Python interpreter at /usr/bin/python3.9, but future installation of
another Python interpreter could change the meaning of that path. See https://docs.ansible.com/ansible-
core/2.15/reference_appendices/interpreter_discovery.html for more information.
changed: [node02]
[WARNING]: Platform linux on host node01 is using the discovered Python interpreter at /usr/bin/python3.9, but future installation of
another Python interpreter could change the meaning of that path. See https://docs.ansible.com/ansible-
core/2.15/reference_appendices/interpreter_discovery.html for more information.
changed: [node01]
[WARNING]: Platform linux on host node03 is using the discovered Python interpreter at /usr/bin/python3.9, but future installation of
another Python interpreter could change the meaning of that path. See https://docs.ansible.com/ansible-
core/2.15/reference_appendices/interpreter_discovery.html for more information.
changed: [node03]

TASK [start & enabled httpd] *********************************************************************************************************
changed: [node03]
changed: [node02]
changed: [node01]

PLAY RECAP ***************************************************************************************************************************
node01                     : ok=2    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node02                     : ok=2    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node03
```

