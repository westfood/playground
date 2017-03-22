# Aplikace - Stručný a výstižný podtitul

## Popis aplikace

### Účel aplikace

### Popsání komponent

OS: Centos 7

## Vagrant - lokální testovací/vývoje prostředí

### Účel Vagrantu

Vagrant umožňuje snadno testovat aplikaci v prostředí identickém s produkčním nasazením. Řeší jak instalaci OS do VM, tak jejich prosíťování a provizi.
Ansible je automatizační nástroj, které úvadí stroje do stavu definovaného ve svých playbooks. Tj. nainstaluje aplikaci dle playbook.
Na pracovním stroji nám Vagrant a Ansible nám umožňuje snadno celé prostředí zničit příkazem vagrant destroy a znovu postavit příkazem vagrant up.
Při nasazení na produkci již Vagrant není třeba, Ansible se ale postará o uvedení produkčního prostředí do požadovaného stavu.

### Závislosti
ansible 2.2.0.0 | http://docs.ansible.com/ansible/intro_installation.html
vagrant | https://www.vagrantup.com/docs/installation/
virtualbox | https://www.virtualbox.org

Na OSX je ideální použít package manager brew. Obecně statí použít python pip na instalaci Ansible. Vagrant a virtualbox nainstalovat z repozitáře distribuce.

### Užití
vagrant up nahodí zpravidla box 'centos/7' a ansible do něj nainstaluje základní konfiguraci
```
git clone git@bitbucket.org:nlcr/aplikace.git
cd aplikace
vagrant up
```

### Přístupy
všechna uživatelská jména a hesla jsou zpravidla: vagrant

uživatelé je možné definovat v ansible/group_vars/vagrant_machine/vars

## Použití na produkci

### Spuštění na produkci

```
ansible-playbook site.yml -i hosts-production
```

### Ansible vault, přístup k zašifrovaným souborům
Pro přístup k zašifrovaným souborům (např. ansible/group_vars/vault) očekává ansible heslo. Místo opětovného zadávání hesla, stačí vyexportovat proměnou VAULT_PASSWORD s heslem. Skript vault_pass.py heslo dodá z prostředí.

~.zshrc nebo ~/.bash_profile přidat řádek proměnou

```
export VAULT_PASSWORD='Tajná proměná kterou dostanu od správce produkčního prsotředí, např. od Rudolfa'
```

## Popis řešení
