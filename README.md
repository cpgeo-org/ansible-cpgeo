ansible-pull -U https://github.com/cpgeo-org/ansible-mate24.git -e 'ip=192.168.0.16 extras=true' cliente_nis.yml cliente_nfs.yml tela_de_login.yml

ansible-pull -U https://github.com/cpgeo-org/ansible-mate24.git rede.yml cliente_nis.yml cliente_nfs.yml tela_de_login.yml instalar_apps.yml

ansible workstations -i inventario.ini -ku root -m ping

ansible-playbook -i inventario.ini -ku root atualizar_apps.yml

ansible workstations -i inventario.ini -ku root -m import_tasks -a "file=atualizar_apps/nomachine.yml"


ansible-playbook -i inventario.ini -ku root atualizar_apps.yml

ansible-playbook -i "192.168.0.232," -ku root 03_cliente_ldap.yml


# Reinstalar cliente NIS
sudo ansible-playbook -l localhost -e 'is_ubuntu_24=false is_mint_22=true' -u root 03_cliente_nis.yml

# Reparar login
sudo ansible-playbook -l localhost -u root corrigir_login.yml
