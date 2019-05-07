### Azure login using powershell
Using password file to login for furture full automation
------
1. Save the login credential into AES file.
   Use Get-Credential -username and hold the credential into memory

  ```powershell
      $MyAzureLogin = Get-Credential -username '123user@123.com' -Message 'Login to Azure' 
  ```
        this will prompt a interactive login screen. put your password here and click ok, 
        then the dialog disappeared and your credential are safely holded in your variable $MyAzureLogin.
        

2. Generate an AES Key and save the key into filesystem
```powershell
     $theKey = new-object Byte[] 32 # it is either 16 bytes (128 bits), 24 bytes (192 bits), 32 bytes (256 bits)
     [Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($theKey)
     sc ./.AesKey $thekey
```
    

3. save $MyAzureLogin in to file named azure.txt and using the AES key the hash it
  ```powershell 
     $psd = $MyAzureLogin.password | convertfrom-Securestring -key $thekey
     add-content ./.passwd.txt $psd
     add-content ./.username.txt $MyAzureLogin.username
  ```

4. the retrieve the password, aes key and user name
```powershell
   $username = gc ./.username.txt
   $psd = $(gc ./.passwd.txt) | convertto-SecureString -Key $(gc ./.Aeskey) 
   $cred = new-object System.management.Automation.PSCredential -Argumentlist $username, $psd
```

5. Login to Azure in powershell 
```powershell
   Login-AzureRmAccount -Credential $cred
```
   
[Thanks Daivd Lee's work] https://blog.kloud.com.au/2016/04/21/using-saved-credentials-securely-in-powershell-scripts/
