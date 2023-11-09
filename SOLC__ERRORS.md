
# PROBLEM NO 1 : HOW TO USE REMAPPINGS IN SOLC COMPILER ?

**openzeppelin example**
```
$ solc .  @openzeppelin=node_modules/@openzeppelin ./PATH/FILE.sol
```



# PROBLEM NO 2: HOW TO NOT GET SOLC IMPORT ERRORS ?
- You either move everything to subdirectory from root
- Or Simply You Use Crytic-compile to do your job
- Thirdly You dont Need To, You Must Do foundry compiling and then rely on echidna

