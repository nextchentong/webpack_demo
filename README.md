# webpack_demo

# package.json 与 package-lock.json 的区别

package.json 这个文件是 npm init 时创建的一个文件，会记录当前整个项目中的一些基础信息。而 package-lock.json 这个文件却是 node_modules 文件夹或者 package.json 文件发生变化时自动生成的。这个文件主要功能是确定当前安装的包的依赖，以便后续重新安装的时候生成相同的依赖，而忽略项目开发过程中有些依赖已经发生的更新。

自 npm 5.0 版本发布以来，npm i 的规则发生了三次变化。

1、npm 5.0.x 版本，不管 package.json 怎么变，npm i 时都会根据 lock 文件下载
　　　　 package-lock.json file not updated after package.json file is changed · Issue #16866 · npm/npm
　　　 这个 issue 控诉了这个问题，明明手动改了 package.json，为啥不给我升级包！然后就导致了 5.1.0 的问题...

2、5.1.0 版本后 npm install 会无视 lock 文件 去下载最新的 npm
　　　　 why is package-lock being ignored? · Issue #17979 · npm/npm
　　　 这个 issue 控诉这个问题，最后演变成 5.4.2 版本后的规则。

3、5.4.2 版本后 why is package-lock being ignored? · Issue #17979 · npm/npm
　　　 大致意思是，如果改了 package.json，且 package.json 和 lock 文件不同，那么执行`npm i`时 npm 会根据 package 中的版本号以及语义含义去下载最新的包，并更新至 lock。

如果两者是同一状态，那么执行`npm i`都会根据 lock 下载，不会理会 package 实际包的版本是否有新。
