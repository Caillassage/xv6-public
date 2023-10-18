# TP1

```
make qemu-nox
```

### Question 1
1. fichier  sysfile.c
2. static int (*syscalls[])(void), fichier syscall.c. il récupère le n° de la primitive via le fichier syscall.h.

trap -> syscall() -> sys_<>(void)

### Question 2
1. concatène `SYS_` à `name`. Cela permet de faire appel au n° primitive dans syscall.h. 
```
#define SYSCALL(name) \
  .globl name; \
  name: \
    movl $SYS_ ## name, %eax; \
    int $T_SYSCALL; \
    ret
```
2. Un proto de fonction permet d'appeler la fonction dans d'autres fichiers. On remplace off_t par int, car off_t peut être négatif. En pratique, il faudrait utiliser un long int (car avec int, max 2Gb, pas suffisant).
3. On définit ces constantes dans fcntl.h

# TP2

### Question 1
**Numéro de majeur** : numéro de driver
**Numéro de mineur** : numéro de périphérique
3. `ls` fourni par xv6 affiche le type de l’inode, soit 3 pour les fichiers périphériques.