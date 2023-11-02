
# AppServer POC Setup Manual

## Prerequisites

- Windows Systeem met minimum 8GB RAM
- Virtualisatie moet enabled zijn. Dit kan je controleren door naar de Taskmanager(Taakbeheer) te gaan. CTRL+ALT+DEL of via de Windows zoekfunctie. Ga nu naar Performance(Prestaties) en daar zal je Virtualisation op ingeschakeld of uitgeschakeld zien staan. Als je virtualisatie niet ziet staan dan wil dit zeggen dat jouw PC dit niet ondersteund en kan je deze manual ook niet voltooien. Als virtualisatie uitgeschakeld staat, dan zal je dit moeten aanzetten in de BIOS. Om naar de BIOS te gaan zal dit afhangen van de desktop/laptop van de gebruiker. 

![VirtualisatieCheck](img/VirtualisatieEnabled.png)

- indien Hyper-V aanstaat, schakel deze dan uit. Dit kan je doen in de Windows onder Programs and features. Schakel Windows Hypervisor Platform of Hyper-V uit.

![HyperVCheck](img/HyperVCheck.png)

- Installaties:
  - git: <https://git-scm.com/>
  - VirtualBox + guest additions: <https://www.virtualbox.org/>
  - Vagrant: <https://www.vagrantup.com/>
    
- Installatie kan ook aan de hand van 'Chocolatey': <https://chocolatey.org/> <br>
Open CMD of Powershell als **administrator**
```
choco install git -y
choco install virtualbox --version 6.1.40 -y
choco install vagrant --version 2.2.16 -y
```
***Na installatie zal er gevraagd worden om een reboot te doen***


## Appserver VM + container opstarten

Open **CMD** of **Powershell** door op de Windows toets te duwen en CMD of Powershell in te geven.  
Navigeer naar de volgende folder \devops-23-24-operations-t01\src\1.TestOmgeving\Code aan de hand van het "cd" commando. 

Het enige wat je nu hoeft te doen is "Vagrant up appsrv01" in te geven. Alles zal nu automatisch geconfigureerd worden. Dit neemt ongeveer 3-4 minuten in beslag. 

```
vagrant up appsrv01
```

## Github Repo
Clone deze repository naar een map op jouw VM na dat je vagrant ssh appsrv01 hebt uitgevoerd: 

```
git clone https://github.com/jellejacobs/POC
```
## AppServer
vervolgens gaan we naar de juist locatie in onze map naar /POC/src/docker/AppServer
```
cd POC/src/docker/AppServer
```
Hierna gaan we onze AppServer builden met volgend commando:
```
sudo docker build . -t appserver
```
Om nu onze AppServer te runnen voeren we volgend commando uit:
```
sudo docker run --env-file env -ti -p 192.168.10.4:80:80 appserver
```
Vervolgens kunnen we in onze SQL server zien dat de sports databank is aangemaakt.  
![image](https://github.com/HOGENTDevOpsPrj/devops-23-24-operations-t01/assets/58846357/b7f81605-fb2e-4fda-9473-d6d87e6005e9)

Wanneer we nu surfen in de browser naar 192.168.10.4 komt de website tevoorschijn.
![image](https://github.com/HOGENTDevOpsPrj/devops-23-24-operations-t01/assets/58846357/fef02243-44ab-4a32-b0cb-6aeaeba3043a)



