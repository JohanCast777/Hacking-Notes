

==Clean up the flash driver==

```
diskpart
```

```
list disk
```

```
select disk 1
```

```
clean
```

```
create partition primary
```

```
select partition 1
```

```
format fs=fat32
```

Differents formats avaliables

| Filesystem | Max File Size | Max Volume           | Windows | macOS   | Linux         | Best For                                                     |
| ---------- | ------------- | -------------------- | ------- | ------- | ------------- | ------------------------------------------------------------ |
| **FAT32**  | 4GB           | 8TB (32GB practical) | ✅ R/W   | ✅ R/W   | ✅ R/W         | **Maximum compatibility** (old devices, TVs, game consoles)  |
| **exFAT**  | 16EB          | 128PB                | ✅ R/W   | ✅ R/W   | ✅ R/W*        | **Large files + cross-platform** (>4GB videos, flash drives) |
| **NTFS**   | 16EB          | 16EB                 | ✅ R/W   | ✅ Read* | ✅ Read/Write* | **Windows-only** (security, compression)                     |
| **FAT**    | 4GB           | 2TB                  | ✅ R/W   | ✅ R/W   | ✅ R/W         | Legacy devices (very old systems)                            |
| **ReFS**   | 16EB          | 16EB                 | ✅ R/W   | ❌       | ❌             | Windows servers (data integrity)                             |

```
assign letter=H
```

```
exit
```

Let's see the OS to install and look it up

![[Pasted image 20260118145957.png]]

Check the signature of the application

[[ᝰ✍🏻VERIFYCATION SIGNATURE STEPS]]

Install the tools to boot the usb can be ([Rufus](https://rufus.ie/es/),[Balena Etcher](https://etcher.balena.io/),[Ventory](https://www.ventoy.net/en/index.html), [UNetbootin](https://unetbootin.github.io/))

Configure the USB booteable creator 
![[Pasted image 20260118222029.png]]



