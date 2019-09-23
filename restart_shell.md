#!/bin/bash

mqid=`ps -aux | grep xxx.php | grep -v grep | wc -l`

if [ "$mqid" = 0 ]
then
    `nohup php xxx.php > nohup.out 2>&1 &`
fi