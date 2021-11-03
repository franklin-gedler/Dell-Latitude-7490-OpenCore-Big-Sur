# Dell Latitude 7490 - MacOS Big Sur

_Herramientas:_

* Para montar la particion EFI: [MountEFI] https://github.com/corpnewt/MountEFI
* Para configurar config.plist: https://github.com/corpnewt/ProperTree
* Para Generar SMBios: https://github.com/corpnewt/GenSMBIOS


_Config Bios:_
```
Boot mode: UEFI
SecureBoot = Disable
SATA Mode: AHCI 
Intel SGX: Software Controlled
```

_Crear USB boot_
```
sudo /Applications/Install\ macOS\ Big\ Sur.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
```

_Descargamos la carpeta EFI preconfigurada_

* [EFI.zip](https://drive.google.com/file/d/11TnC5klyfgk6HuCEZ8gkkf6kjhhyMvx6/view?usp=sharing)
* Montamos la Particion EFI del USB-BOOT y pegamos la carpeta EFI descargada


_Ejecutamos el pendrive y en el arranque seleccionamos modGRUBShell.efi_

```
CFG Lock = Disable
    (VarOffset/VarName): 0x52D
    VarStore: 0x1
    Name: Setup
    
    Comando para modGRUBShell.efi: setup_var_cv Setup 0x52D 0x1 0x0
____________________________________________________________________

DVMT Pre-Allocated = 64MB
    (VarOffset/VarName): 0x804
    VarStore: 0x1
    Name: Setup
    
    Comando para modGRUBShell.efi: setup_var_cv Setup 0x804 0x1 0x2
____________________________________________________________________

DVMT Total Gfx Mem = Max
    (VarOffset/VarName): 0x805
    VarStore: 0x1
    Name: Setup
    
    Comando para modGRUBShell.efi: setup_var_cv Setup 0x805 0x1 0x3
____________________________________________________________________

VT-d = Disable
    (VarOffset/VarName): 0x808
    VarStore: 0x1
    Name: Setup
    
    Comando para modGRUBShell.efi: setup_var_cv Setup 0x808 0x1 0x0
```
* Despues de ejecutar los comandos APAGAMOS la maquina

* Ejecutamos de nuevo el USB-BOOT e instalamos normalmente

* Una vez iniciado el escritorio de Big Sur descargamos la herramienta https://github.com/corpnewt/MountEFI para montar la particion EFI del Disco Interno y del USB-BOOT

* Copiamos la carpeta EFI de USB-BOOT y la pegamos en la particion EFI del disco interno

* Desconecamos el USB-BOOT y reiniciamos asi vemos que inicie normalmente

* Recuerda generar un nuevo SMBios https://github.com/corpnewt/GenSMBIOS
```
Dentro de GenSMBios:
Seleccionamos opcion 2 y arrastamos el config.plist de la carpeta EFI del disco interno
Seleccionamos opcion 3 asi le inyecta al config.plist el GenSMBios nuevo
```
