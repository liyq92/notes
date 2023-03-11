1.添加用户组

> sudo groupadd ${goupname}

2.添加当前用户到用户组

> sudo usermod -aG docker ${USER}
>
> > * 提示用户不是 sudoers,报告 root 之类的
> >
> >   * 切换 root 用户
> >
> >     > su - root
> >
> >   * 查看 sudoers ,只有读权限
> >
> >     > ls -l /etc/sudoers
> >
> >   * 增加写权限
> >
> >     > chomd u+w /etc/sudoers
> >
> >   * 增加用户
> >
> >     > vi 进去找到:
> >     > \#\# Allow root to run any commands anywhere
> >     >
> >     > root    ALL=(ALL)       ALL
> >     >
> >     > 在下面增加:
> >     >
> >     > liyq    ALL=(ALL)       ALL
> >     >
> >     > :wq 退出
> >
> >   * 还原权限:
> >
> >     > chmod u-w /etc/sudoers
> >
> >   * 切换到用户
> >
> >     > su - liyq

3.重启 docker 服务

> sudo systemctl restart docker

4.执行 docker 命令

> 如果还是有问题,退出当前用户,切换 root 用户,在重新登录当前用户

