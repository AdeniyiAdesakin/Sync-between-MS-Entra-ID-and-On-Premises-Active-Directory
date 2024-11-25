<h1>Sync between MS Entra ID & on-premises Active Directory</h1>
<br>
<p>This tutorial outlines steps on how to sync between Microsoft Entra ID and On-Premises Active Directory.</p>
<br>

<p>1. To begin sync between MS Entra ID and On-premises Active Directory, TLS1.2(Transport Layer Security)- a protocol that provides secure communication by encrypting data between clients and servers over a network to protect it from interception and tampering, needs to be enabled. To do this, first right-click start on your windows server and click on Windows Powershell and run this command to enable TLS 1.2 -

  # TLS 1.2 Registry Key
  # https://docs.microsoft.com/en-us/azure/active-directory/hybrid/reference-connect-tls-enforcement#powershell-script-to-enable-tls-12

  New-Item 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319' -Force | Out-Null

	New-ItemProperty -path 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319' -name 'SystemDefaultTlsVersions' -value '1' -PropertyType 'DWord' -Force | Out-Null

	New-ItemProperty -path 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319' -name 'SchUseStrongCrypto' -value '1' -PropertyType 'DWord' -Force | Out-Null

	New-Item 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -Force | Out-Null

	New-ItemProperty -path 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -name 'SystemDefaultTlsVersions' -value '1' -PropertyType 'DWord' -Force | Out-Null

	New-ItemProperty -path 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -name 'SchUseStrongCrypto' -value '1' -PropertyType 'DWord' -Force | Out-Null

	New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Force | Out-Null
	
	New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'Enabled' -value '1' -PropertyType 'DWord' -Force | Out-Null
	
	New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'DisabledByDefault' -value 0 -PropertyType 'DWord' -Force | Out-Null
	
	New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Force | Out-Null
	
	New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'Enabled' -value '1' -PropertyType 'DWord' -Force | Out-Null
	
	New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'DisabledByDefault' -value 0 -PropertyType 'DWord' -Force | Out-Null
	Write-Host 'TLS 1.2 has been enabled.'
 
  <p align="center"><img src="https://i.imgur.com/027NXZ7.png" height="50%" width="50%" alt="image"/>
  <p align="center"><img src="https://i.imgur.com/f47UxJm.png" height="50%" width="50%" alt="image"/>

  <p>2. After the TLS(Transport Layer Security) is enabled, Go to Azure portal on your browser, search for Microsoft Entra connect. </p>
  <p align="center"><img src="https://i.imgur.com/rQlvqCg.png" height="50%" width="50%" alt="image"/>

  <p>3. From the Microsoft Entra Connect, go to Connect Sync, from the connect sync, click on Download Microsoft Entra Connect.</p>
  <p align="center"><img src="https://i.imgur.com/Zdb7GkU.png" height="50%" width="50%" alt="image"/>

  <p>4. After the download is done, go to where the file is downloaded and double click to start the installation.</p>
  <p align="center"><img src="https://i.imgur.com/mOtnUIo.png" height="50%" width="50%" alt="image"/>

  <p>5. After the installation is finished, click on FINISH.</p>
  <p align="center"><img src="https://i.imgur.com/7exsTVT.png" height="50%" width="50%" alt="image"/>
  <p align="center"><img src="https://i.imgur.com/iKxXRXk.png" height="50%" width="50%" alt="image"/>

  <p>6. After the installation, open the Azure AD connect application. Agree to the license terms and privacy notice and click Continue</p>
  <p align="center"><img src="https://i.imgur.com/8LvwK79.png" height="50%" width="50%" alt="image"/>

  <p>7. On the next screen, click on “Use express settings”.</p>
  <p align="center"><img src="https://i.imgur.com/X4tMV6K.png" height="50%" width="50%" alt="image"/>

  <p>8. Then input your Azure credentials(make sure its an Global administrator account) and password, then click NEXT.</p>
  <p align="center"><img src="https://i.imgur.com/vOC6eUZ.png" height="50%" width="50%" alt="image"/>

  <p>9. Next, put in your  On-premises Active Directory credentials(An Administrator account and Password).</p>
  <p align="center"><img src="https://i.imgur.com/m5XSP0T.png" height="50%" width="50%" alt="image"/>

  <p>10. On the “Azure Sign-in configuration screen”, click NEXT</p>
  <p align="center"><img src="https://i.imgur.com/je4HWdw.png" height="50%" width="50%" alt="image"/>

  <p>11. On the “Ready to configure screen”, click on INSTALL. Then you are greeted with the Configuring screen. This may take a while, just wait for it to finish.</p>
  <p align="center"><img src="https://i.imgur.com/0VqB08t.png" height="50%" width="50%" alt="image"/>

  <p>12. After the configuration is done, you will see a “Configuration Complete” message, click EXIT.</p>
  <p align="center"><img src="https://i.imgur.com/Whfa4uw.png" height="50%" width="50%" alt="image"/>

  <p>13. To confirm that the Sync is complete, go back to your Azure portal and go to Microsoft Entra ID, then Users, you will see the On Premises users have been added to your Microsoft Entra ID users.</p>
  <p align="center"><img src="https://i.imgur.com/XV3Ixdy.png" height="50%" width="50%" alt="image"/>

  <br>

