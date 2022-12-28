---
title: Recuperar Grub
created: 2022-12-27T00:00:00.000Z
update: 
tags:
  - grub
---

# Recuperar Grub

Após fazer um dual boot com o Windows o Grub do Linux some e se perde acesso as outras distribuições não windows, para recuperar basta seguir esses passos.

## Requisitos

- mídia física com distribuição qualquer linux

## Passos

Insira o pendrive no computador e boot pela live.

Identifique em qual partição o linux está instalado. 

```
$ sudo fdisk -l
```
```
...

Device     Boot     Start       End   Sectors   Size Id Type
/dev/sda1            2048 488978431 488976384 233,2G  7 HPFS/NTFS/exFAT
/dev/sda2  *    488978434 976769023 487790590 232,6G 83 Linux
```

Na coluna `Type` é possível identificar pelo tipo `Linux` e na `Device` mostra o local.

Em seguida, com o comando `mount` monte a partição `sdx` (Substitua o `x`) passando a flag `-t ext4` em `/mnt`.

```
$ sudo mount -t ext4 /dev/sdx /mnt
```

Agora basta utilizar o comando `grub-install` e passar para a flag `--root-directory` o local onde montou a partição, no caso `/mnt` e a partição.

```
$ sudo grub-install --root-directory=/mnt /dev/sdx
```

Agora é só reiniciar o computador.

```
$ restart
```