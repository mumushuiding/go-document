
# 第一步：设置 dockerfile

FROM scratch

ADD /app //                   // app是 go build 生成的可执行文件

ADD /config.json //           // config.json 是根目录下的配置文件

ENTRYPOINT ["/app"] 

--------------
# 第二步： 进入go 项目所在的根目录

# 第三步：设置环境变量

---------  在控制台执行以下命令，否则无法生成二进制可执行文件--------

SET CGO_ENABLED=0

SET GOOS=linux

SET GOARCH=amd64

go env     // 查看环境变量是否设置成功，命令行在powershell模式下可能会失败，需要切换成cmd模式

# 第四步：编译

go build

# 第五步：打包成镜像

$ docker build . -t my-app

$ docker push my-app // 推送到远程镜像服务器

# 第六步：运行

$ docker run  -p 8080:8080 my-app