create **config.yaml** with this entry



```

cryticArgs: ['--solc-remaps', '@=node_modules/@']

```

**Multiple remappings**

```
cryticArgs: ['--solc-remaps', 'remapping(1) remapping(2) remapping(3) ..... remapping(N)']
```

**example**
```
cryticArgs: ['--solc-remaps', '@y/=src/a/y/ @z/=src/b/z/']
```

