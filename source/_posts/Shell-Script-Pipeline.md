---
title: Shell Script Pipeline
date: 2020-12-03 17:02:49
tags:
---

最近在工作中经常会遇到任务流控制相关的任务，总结一套shell 任务流控制的脚本模板
```bash
#!/usr/bin/env bash

# 该脚本主要用于pipeline任务的执行。如任务分为3步：
# step 1: xx
# step 2: xx
# step 3: xx
# 用法:
# ./run.sh 1-3  执行1-3步任务
# ./run.sh 1,2,4  执行1,2,4步任务

cmd_seq=$1


function parse_task_seq() {
  if [[ "${cmd_seq}" == *"-"* ]]; then
    # shellcheck disable=SC2206
    pipeline_seq=(${cmd_seq//-/ })
    start_step=${pipeline_seq[0]}
    end_step=${pipeline_seq[1]}
    # shellcheck disable=SC2207
    step_seq=($(seq "$start_step" "$end_step"))
  else
    # shellcheck disable=SC2206
    step_seq=(${cmd_seq//,/ })
  fi
  return "${step_seq[@]}"
}

function pipeline_controller() {
  echo "run ${#step_seq[@]} task: ${step_seq[*]}"
  for step in "${step_seq[@]}";
  do
    echo "[$(date +"%y-%m-%d %H:%M:%S")] Task[$step] Starts running..."
    had_task_handle=1
    if [ "$step" -eq 1 ]
    then
      echo "1"

    elif [ "$step" -eq 2 ]
    then
      echo "2"
    elif [ "$step" -eq 3 ]
    then
      echo "3"
    else
      had_task_handle=0
    fi

    if [ $had_task_handle -eq 1 ]
    then
      echo "[$(date +"%y-%m-%d %H:%M:%S")] Task[$step] Running done."
    else
      echo "[$(date +"%y-%m-%d %H:%M:%S")] Task[$step] Has no handler."
    fi
  done
}

parse_task_seq
pipeline_controller

```