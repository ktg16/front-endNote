```
vue-cli-service build --no-clean
```

vue-cli 打包让其不删除dist里的原有文件

有个`build.emptyOutDir`，设为 false 即可，或者 `npm build --emptyOutDir=false`。
[build-emptyoutdir]( https://cn.vitejs.dev/config/#build-emptyoutdir)