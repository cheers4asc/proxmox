# proxmox
## Nested Virtulization
In order to enable the Nested Virtulization
You will update the "/etc/pve/qemu-server/*.conf" file\
You will add a following line to the file \
`cpu: cputype=host`
Please make sure the Host machine has virtulization enabled

reference:- https://pve.proxmox.com/wiki/Manual:_qm.conf <br />
            https://pve.proxmox.com/wiki/Nested_Virtualization
