# Select a subscription using default dialogue
```powershell
Select-Azurermsubscription -subscription $(get-azurermsubscription | ogv -outputmode single)
```
##### A dialogue will then shown click on the subscription you need then click "ok" at the lower right corner
