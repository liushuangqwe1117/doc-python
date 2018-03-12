## python编辑器

### IDLE编辑器
1.快捷键Atl + G 可以快速定位到指定行,在编辑器右下角有显示光标所在行号列号

### PyCharm编辑器
1. 设置开发环境的文件编码为unix系统编码，避免部署时出现行尾^M符号

  ![](/images/pycharmlineseperator.png)

  ![](/images/pycharmlineseperator2.png)

  如果已经将文件上传到了linux服务器上，则可以通过linux中的dos2unix命令进行批量转换
  ```
  [root@hz ~]# dos2unix  *.log
  dos2unix: Binary symbol found at line 2
  dos2unix: Skipping binary file lnmp-install.log
  [root@hz ~]#

  ```
