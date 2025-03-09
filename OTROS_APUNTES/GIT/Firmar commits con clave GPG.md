
**1.- Ejecutar el comando:**

```shell
gpg --full-generate-key
```

(Te pedirá que elijas el tipo de clave, generalmente selecciona `RSA` con una longitud de al menos **4096 bits.** Para Windows, es recomendable instalar [GPG4Win](https://gpg4win.org/), que facilita el uso de GPG en este sistema.)

**2.- Obtener ID de clave GPG**

```shell
gpg --list-secret-keys --keyid-format LONG`
```
``
Ejemplo:
```
`/home/user/.gnupg/secring.gpg ------------------------------ sec   4096R/<YOUR_KEY_ID> 2024-10-26 [expires: 2026-10-25]`
```

Para configurar Git y firmar tus commits en GitHub, necesitas el **ID de la clave principal** (la que aparece después de `sec`).

**3.- Exportar clave pública**
```shell
gpg --armor --export <YOUR_KEY_ID>
```

**4.- Añadirla a GitHub**
En Github > Configuración > SSH and GPG  Keys >> New GPG Key.

**5.- Usar esta clave para firmar los commits**

```shell
git config --global user.signingkey <YOUR_KEY_ID>
# Para que siempre se firmen
git config --global commit.gpgSign true
# Para firmarlo a voluntad
git commit -S -m "mensaje del commit"
```

**6.- En Jetbrains**
- Navega a **Version Control > Git**.
- En **GPG Key**, introduce el **ID de tu clave GPG** (el mismo que usaste en Git).
- Verifica que el **Git Executable** esté configurado correctamente.
- Selecciona **Use Custom Executable** y define la ruta a `gpg.exe`, por ejemplo:
    `C:\Program Files (x86)\GnuPG\bin\gpg.exe`


----
----


![[Pasted image 20250309191732.png]]