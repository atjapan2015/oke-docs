[返回OKE中文文档集](../README.md)

# OKE节点内核优化

OKE节点内核优化。
在创建Pool时，在"show advanced options"的"Initialization script"里面输入下面脚本内容，具体优化内容请根据实际情况调整。

```
#!/bin/bash
curl --fail -H "Authorization: Bearer Oracle" -L0 http://169.254.169.254/opc/v2/instance/metadata/oke_init_script | base64 --decode >/var/run/oke-init.sh
bash /var/run/oke-init.sh

cat <<EOF > /etc/security/limits.d/20-nproc.conf
*          soft    nproc     65535
*          hard    nproc     65535
root       soft    nproc     unlimited
root       hard    nproc     unlimited
EOF

cat <<EOF > /etc/security/limits.d/20-nofile.conf
*          soft    nofile     65535
*          hard    nofile     65535
root       soft    nofile     65535
root       hard    nofile     65535
EOF

sleep 3s
reboot
```

[返回OKE中文文档集](../README.md)

