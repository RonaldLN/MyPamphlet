## 1

由于ros需要使用的是ubuntu系统自带的python，而我的ubuntu系统之前装了anaconda，所以在 `rosrun` 

打开 `~/.bashrc` 文件，将

```bash
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/home/ronald/anaconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home/ronald/anaconda3/etc/profile.d/conda.sh" ]; then
        . "/home/ronald/anaconda3/etc/profile.d/conda.sh"
    else
        export PATH="/home/ronald/anaconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

注释掉

![anaconda_conflict](../images/anaconda_conflict.png){ loading=lazy }

