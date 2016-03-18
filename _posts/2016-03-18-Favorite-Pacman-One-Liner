---
layout: post
title: Favrote Pacman One Liner
---

Today while doing some system maintenance I realized that I have
never removed any dependencies that are left behind by pacman
when it removes programs. So after so quick Googling of the available
pacman commands I came up with this awesome one liner that removes all
dependencies that are not needed anymore.

[code]
pacman -Rns $(pacman -Qtdq)
[/code]
