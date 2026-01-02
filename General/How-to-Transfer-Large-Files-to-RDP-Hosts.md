# How to Transfer Large Files to RDP Hosts

Use BITS protocol.

[https://woshub.com/copying-large-files-using-bits-and-powershell](https://woshub.com/copying-large-files-using-bits-and-powershell/)

Before you begin, you will need to ensure that the inbound firewall rule, **File and Printer Sharing (SMB-In)**, is enabled and configured to allow your IP address.

Any folder that you transfer to needs to be shared. It seems that a user's home directory is shared by default, but check to make sure.

Transfer a file:
`Start-BitsTransfer -source .\RTACSetup.exe -destination \\10.162.14.35\Downloads -asynchronous -Priority low -Authentication NTLM -Credential CEGAdmin -DisplayName "RTAC Setup"`

Check on the status of the transfer:
`Get-BitsTransfer | fl`

Finish the transfer so that it shows up in the folder you sent it to:
`Get-BitsTransfer | Complete-BitsTransfer`

Clear all transfers that were in the queue:
`Get-BitsTransfer -Allusers | Remove-BitsTransfer`
