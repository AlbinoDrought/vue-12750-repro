# Reproduce https://github.com/vuejs/vue/issues/12750

- `vue create` with this preset: Babel, Typescript (class component), Linter

```json
{
  "useTaobaoRegistry": false,
  "latestVersion": "5.0.8",
  "lastChecked": 1666036674630,
  "presets": {
    "vue-12750-repro": {
      "useConfigFiles": true,
      "plugins": {
        "@vue/cli-plugin-babel": {},
        "@vue/cli-plugin-typescript": {
          "classComponent": true,
          "useTsWithBabel": true
        },
        "@vue/cli-plugin-eslint": {
          "config": "base",
          "lintOn": [
            "save"
          ]
        }
      },
      "vueVersion": "2"
    }
  }
}
```

- Install vuelidate and types: `npm install --save @types/vuelidate vuelidate`

- Add vuelidate to a component: [see HelloWorld.vue](./src/components/HelloWorld.vue)

- Try to build: `npm run build`:

```
RangeError: Maximum call stack size exceeded
    at getMappedType (/vue-12750/node_modules/typescript/lib/typescript.js:61620:31)
    at getMappedType (/vue-12750/node_modules/typescript/lib/typescript.js:61637:30)
    at getMappedType (/vue-12750/node_modules/typescript/lib/typescript.js:61637:30)
    at /vue-12750/node_modules/typescript/lib/typescript.js:61768:82
    at Object.map (/vue-12750/node_modules/typescript/lib/typescript.js:652:29)
    at getObjectTypeInstantiation (/vue-12750/node_modules/typescript/lib/typescript.js:61768:40)
    at instantiateTypeWorker (/vue-12750/node_modules/typescript/lib/typescript.js:61999:28)
    at instantiateTypeWithAlias (/vue-12750/node_modules/typescript/lib/typescript.js:61979:26)
    at instantiateType (/vue-12750/node_modules/typescript/lib/typescript.js:61962:37)
    at instantiateList (/vue-12750/node_modules/typescript/lib/typescript.js:61595:34)
```
