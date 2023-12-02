### Instalare configurar o samba

```bash
sudo apt update
sudo apt install samba
```

#### Verificar se o servico esta rodando corretamente

```bash
sudo systemctl status smbd
```

#### Liberar o Samba no firewall

```
sudo ufw allow 'Samba'
```

#### Permitir que meu usuario acesse o samba

```bash
smbpasswd -a $USER
```

#### Compartilhar uma pasta

Criar uma pasta no local desejado, como `mkdir ~/shared`

Alterar o arquivo /etc/samba/smb.conf, adicionando no final dele uma configuracao para a pasta nova criada

```conf
[network]
  path = /home/user/shared
  browseable = yes
  read only = no
  writable = yes
  create mask = 0775
  directory mask = 0775
  force create mode = 0775
  force directory mode = 0775
  valid users = user1 @group1 @group2
```
#### Reiniciar o samba

```bash
sudo systemctl restart smbd
sudo systemctl restart nmbd
```

### Permitir acesso a pasta compartilhada por outros computadores na rede via cli

Criar uma pasta no local desejado, como `mkdir ~/shared-nome-computador` e montar a pasta

```bash
sudo mount -t cifs //ip-do-computador/nome-da-pasta-compartilhada pasta-local-para-montar -o user=usuarioSamba,password=senhaSamba,uid=usuarioLocal,gid=grupoLocal
```
