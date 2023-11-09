create **config.yaml** with this entry



```

cryticArgs: ['--solc-remaps', '@=node_modules/@']

```

**Multiple remappings**

```

cryticArgs: ['--solc-remaps', '@=node_modules/@', 'github=node_modules/github/@']

```
