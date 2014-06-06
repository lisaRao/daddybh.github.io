Grunt应用
=========
***
##介绍
gruntjs是一个基于nodejs的自动化工具

[Gruntjs官网](http://gruntjs.com/)

[Getting Start](http://gruntjs.com/getting-started)

##安装
* 安装nodejs, nodejs安装包
[(32-bit)](http://nodejs.org/dist/v0.10.28/node-v0.10.28-x86.msi), [(64-bit)](http://nodejs.org/dist/v0.10.28/x64/node-v0.10.28-x64.msi)

* 安装gruntjs
    >npm install -g grunt-cli

* 定位到你项目目录 
    > cd d:\www\branches\applepc\ios_v2

* 初始化，根据提示输入项目信息，初始化完成后，会自动生成package.json文件
    >npm init

* 项目根目录，添加Gruntfile.js（文件名`区分`大小写）, Gruntfile.js内容基本结构如下：
    ```
    module.exports = function(grunt) {
        grunt.initConfig({
           
        });
    
        grunt.loadNpmTasks('grunt-contrib-uglify');
        
        grunt.registerTask('default', ['uglify']);
    
    }
```
    

* 通过npm install 安装你需要的插件, 例如

    >npm install grunt-contrib-copy

    >npm install grunt-contrib-watch

* 回到Gruntfile.js中，为新安装的插件添加任务
```
    module.exports = function(grunt) {
        grunt.initConfig({
           copy:{//配置copy任务，详细配置信息，请参考grunt-contrib-copy github页
                main:{
                    files:[
                        {
                            cwd: 'common/tpl/appDetails/compiled/',
                            src: 'template.js',
                            dest: 'common/js/bcvy6gt37&[8fgt4!3$8gfg82799/',
                            expand: true,
                            rename : function(dest, src){
                                return dest + "appDetailsTpl.js";
                            }
                        }
                    ]
                }
            }
        });
    
        grunt.loadNpmTasks('grunt-contrib-uglify');
        grunt.loadNpmTasks('grunt-contrib-copy');//加载任务
        
        grunt.registerTask('default', ['uglify']);
        grunt.registerTask('copy', ['copy']);//注册复制任务
    
    }
```

* 运行`grunt copy`就可以执行复制任务

* 自定义任务, grunt支持自定义任务，以腾讯tmod为例，请参考下面代码片段, 运行`grunt ct`可执行simple ArtTemaplte模板预编译
```
    module.exports = function(grunt) {
        grunt.initConfig({
           copy:{//配置copy任务，详细配置信息，请参考grunt-contrib-copy github页
                main:{
                    files:[
                        {
                            cwd: 'common/tpl/appDetails/compiled/',
                            src: 'template.js',
                            dest: 'common/js/bcvy6gt37&[8fgt4!3$8gfg82799/',
                            expand: true,
                            rename : function(dest, src){
                                return dest + "appDetailsTpl.js";
                            }
                        }
                    ]
                }
            }
        });

        grunt.registerTask('ct', 'complie template', function() {
            var TmodJS = require("tmodjs");
            var path = './common/tpl/appDetails/';
            var options = {
                output: 'compiled',
                helpers:'helpers.js',
                charset: 'utf-8',
                debug: false // 此字段不会保存在配置中
            }
            TmodJS.init(path, options);
            TmodJS.compile([], true);
        });
    
        grunt.loadNpmTasks('grunt-contrib-uglify');
        grunt.loadNpmTasks('grunt-contrib-copy');//加载任务
        
        grunt.registerTask('default', ['uglify']);
        grunt.registerTask('copy', ['copy']);//注册复制任务
    
    }
```

##常见插件

* `grunt-contrib-uglify` 文件压缩工具 （[github](https://github.com/gruntjs/grunt-contrib-uglify)）
* `grunt-contrib-copy` 文件复制  （[github](https://github.com/gruntjs/grunt-contrib-copy)）
* `grunt-css-sprite` 从css文件中提取图片，生成雪碧图 ([github](https://github.com/laoshu133/grunt-css-sprite))
* `grunt-contrib-watch` 检测文件变化，然后执行相应的任务 ([github](https://github.com/gruntjs/grunt-contrib-copy))
* 更多插件，请参考官网([Grunt.js官网插件页](http://gruntjs.com/plugins))
