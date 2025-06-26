# Parameter die hinter der ps1 geschreiben werden
param (
    [switch]$joinDomain, [switch]$update
)
$Hardware = Get-NetAdapter 

if($hardware -eq $null)
{
write-host "keine hardware gefunde.. Installiere"
pnputil /add-driver f:\netkvm\2k19\amd64\netkvm.inf /install
pnputil /add-driver f:\balloon\2k19\amd64\balloon.inf /install
}else{
write-host " hardware gefunden.. weiter gehts"
}

#eingaben die in variablen gespeichert werden
$ip = Read-Host "IP-Adresse eingeben"
$gw = Read-Host "IP für Gateway eingeben"
$dns = Read-Host "IP für den DNS Server eingeben"
$name = Read-Host "Name für den Rechner angeben"
$domain = Read-Host "Bei Einladung in eine Domäne,den Domänenname eingeben"
$netadapter = Get-NetAdapter
$aindex =$netadapter[0].ifIndex
$aname = $netadapter[0].name

#ändern der grundkonfig
Rename-Computer -NewName $name
Set-NetIPInterface -InterfaceIndex $aindex -Dhcp disable
New-NetIPAddress -interfacealias $aname -IPAddress $ip -AddressFamily IPv4 -PrefixLength 24 -DefaultGateway $gw
Set-DnsClientServerAddress -Interfacealias $aname -ServerAddresses $dns
Disable-NetAdapterBinding -name $aname -ComponentID ms_tcpip6
netsh advfirewall firewall set rule group="datei- und druckerfreigabe" new enable=yes
netsh advfirewall firewall set rule group="Remotedienstverwaltung" new enable=yes
netsh advfirewall firewall set rule group="Remote-Ereignisprotokollverwaltung" new enable=yes
netsh advfirewall firewall set rule group="Remotevolumeverwaltung" new enable=yes
netsh advfirewall firewall set rule group="Remotedesktop" new enable=yes
netsh advfirewall firewall set rule group="Windows-Remoteverwaltung" new enable=yes
netsh advfirewall firewall set rule group="Netzwerkerkennung" new enable=yes
netsh advfirewall firewall set rule group="Remoteereignisüberwachung" new enable=yes

# --- Remoteverwaltung aktivieren ---
Write-Host "Aktiviere Remoteverwaltung und PowerShell-Remoting..."
Enable-PSRemoting -Force
Set-Item -Path WSMan:\localhost\Service\AllowUnencrypted -Value $true
Set-Item -Path WSMan:\localhost\Service\Auth\Basic -Value $true
winrm quickconfig -force

# --- Remote Desktop aktivieren ---
Write-Host "Aktiviere Remote Desktop..."
Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server" -Name "fDenyTSConnections" -Value 0

# RDP durch die Firewall lassen
Enable-NetFirewallRule -DisplayGroup "Remotedesktop"

# das ist das herunterladen von updates und die instalation. Habs auskommentiert weils zu lange dauert
if ($update){
Install-Module -name PSWindowsUpdate -Force
Get-Wulist
install-windowsupdate -microsoftupdate -acceptall
} 
# das zeugs soll als parameter ausgeführt werden
if ($joinDomain){
    Add-Computer -DomainName $domain -NewName $name -Credential (get-credential)
 }


Shutdown /s /t 5

