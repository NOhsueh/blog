<h1>
通过Git得到项目代码量信息
</h1>

<code>
git log  --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }'
</code>

<h1>
  wsl的安装
<h1>

  
