**解决办法：**
在后面加入代码

`"ignoreDeprecations":"5.0"`

**整体：**
```json
{
  "extends": "@vue/tsconfig/tsconfig.node.json",
  "include": ["vite.config.*", "vitest.config.*", "cypress.config.*"],
  "compilerOptions": {
    "composite": true,
    "types": ["node"],
    "ignoreDeprecations":"5.0"
  }
}
```