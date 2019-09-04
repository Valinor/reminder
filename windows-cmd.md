# Some usefull cmd tips
## Associate network share to letter
net use w: \\int.ofac.ch\OFAC\Collaborateurs\henriet\workspace
## Wait for 1 second
ping localhost -n 1 -w 1000 > nul
## Delete letter association (with network share)
net use w: /d
