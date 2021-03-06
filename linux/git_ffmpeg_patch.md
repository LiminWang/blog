# git for ffmpeg patch

## 设置 git 用户的邮箱和姓名
git config --global user.email "youremail@gmail.com"
git config --global user.name "name"

## 修改 文件后 commit
```
git commit -m "libavcodec/libdavs2.c: Fix for the wrong line size is used"

commit 6fa7b76a10bee65536aa534e411e35c4d685f90e
Author: Limin Wang <youremail@gmail.com>
Date:   Sun Sep 30 18:07:29 2018 +0800

    libavcodec/libdavs2.c: Fix for the wrong line size is used
```


## 生成 patch 文件
$ git format-patch -1 6fa7b76a10bee65536aa534e411e35c4d685f90e

## 增加patch版本息
$ git format-patch -v2 -1 6fa7b76a10bee65536aa534e411e35c4d685f90e

## 检查patch合法性
$ ./tools/patcheck 0001-avcodec-nvenc-add-more-sei-data-support.patch

## 设置 git 的 smtp 参数

```
git config --global sendemail.from "Limin Wang <youremail@gmail.com>"
git config --global sendemail.smtpserver smtp.gmail.com
git config --global sendemail.smtpuser youremail@gmail.com
git config --global sendemail.smtppass pass
git config --global sendemail.smtpencryption tls
git config --global sendemail.smtpserverport 587 

$ cat ~/.gitconfig
 [user]
     email = youremail@gmail.com
     name = Limin Wang
 [sendemail]
     from = youremail@gmail.com
     smtpserver = smtp.gmail.com
     smtpuser = youremail@gmail.com
     smtppass = password
     smtpencryption = tls
     smtpserverport = 587
```

## 发送邮件给 ffmpeg-devel@ffmpeg.org
```
git send-email ../the_patch_file_in_the_dir.patch
git send-email -to ffmpeg-devel@ffmpeg.org -cc cc_email patch_dir/
git send-email --no-chain-reply-to --to=ffmpeg-devel@ffmpeg.org --in-reply-to=message_id
```
输入 ffmpeg-devel 邮箱地址 ffmpeg-devel@ffmpeg.org

## 增加patch版本息
```
git send-email -s -v2 -3
git send-email -s -v2 -3 -cover-letter
```

## 避免cc邮件给自己
```
git config --global sendemail.suppresscc self
```

## 查看状态
发送邮件过一段时间后(邮件没有加入列表时间会长）,在这里能查到
[patch](https://patchwork.ffmpeg.org/project/ffmpeg/list/)

## 查询提交记录
``
git log --since=2019-03-30T00:00:00Z --until 2020-03-30T00:00:00Z --pretty=fuller | grep '^Author:' | sed 's/<.*//' |sort | uniq -c | sort -nr
git log --since=2019-03-30T00:00:00Z --until 2020-03-30T00:00:00Z --pretty=fuller | grep '^Commit:' | sed 's/<.*//' |sort | uniq -c | sort -nr
git shortlog -nse --since="1 years ago"
``


