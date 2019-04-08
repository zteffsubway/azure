# azure login using powershell
1. save the login credential into aes file
  a. Use Get-Credential -username and hold the credential into memory
  ```powershell
      $MyAzureLogin = Get-Credential -username '123user@123.com' -Message 'Login to Azure' 
  ```
        this will prompt a interactive login screen. put your password here and click ok, 
        then the dialog disappeared and your credential are safely holded in your variable $MyAzureLogin.
  b. save $MyAzureLogin in to file 
