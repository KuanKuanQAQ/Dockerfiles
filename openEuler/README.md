Features:

* Based on Ubuntu:22.04
* gcc-12
* Capable of compiling the Linux kernel
* sudo, wget, curl, gdb, qemu-system included
* Oh-my-zsh shell
* Basic Vim configuration
* Git SSH configuration (with slight security risks)

Before building image, you need copy your `id_rsa` to this dir:

```shell
➜  openEuler cp ~/.ssh/id_rsa ./
```

After entering container, you need to `:PlugInstall` in `vim`.
