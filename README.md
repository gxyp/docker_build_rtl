# docker_build_rtl
Docker file and readme to build rtl sdk

## 创建编译环境

cd dockerfile_folder

docker build  -t centos_build .


## 进入docker环境

docker run -d --cpus 4 -m 2048m -v $(pwd):/root/ -p 7788:22 --name centos_RTL centos_build /usr/local/sbin/run.sh

## 修复因Centos版本问题导致的tar包命令错误和过程中的一些bug

### sed -i 's/jcvf/-Jcvf/g' ./rtl819x/users/boa/html/Makefile

### sed -i 's/jxvf/-Jxvf/g' ./rtl819x/users/boa/Makefile

### if have aclocal issue, need run "autoreconf -ivf" in xz folder

### if have cp home romfs/home issue. need mkdir home in rtl819x/target/

