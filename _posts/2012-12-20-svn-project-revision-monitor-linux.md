---
layout: post
title: "Linux监控SVN仓库源码版本更新"
description: "自动获取监控SVN仓库源码最新版本,邮件发送更新日志信息"
tags: [shell, svn, mail, sed, awk]
---
{% include JB/setup %}

###Linux自动获取SVN版更新信息,并发送邮件通知###  


__pmt.sh__

	#!/usr/bin/bash
	################################################################################
	# 自动获取SVN版更新信息,并发送邮件通知
	# 历史记录:
	# 2012-12-20    v1.0    dennis.cpp@gmail.com
	################################################################################

	conf_file=pmt.conf

	# Fields: project#url#revision#mail
	field_size=4
	arr=($(awk -F'#' '{print $1,$2,$3,$4}' $conf_file))

	item_size=$[${#arr[@]}/$field_size]

	while true ; do

		for ((i=0;i<$item_size;i++))
		do
		{
			index=$[i*$field_size]

			prj=${arr[$[index+0]]}
			url=${arr[$[index+1]]}
			rev_old=${arr[$[index+2]]}
			rev_new=$(svn info $url | awk 'NR==8{print $NF}')

			if (( $rev_new > $rev_old ))
			then
				arr[$[index+2]]=$rev_new
				svn log $url -r $rev_new:$rev_old > svn.log

				subject="[svn monitor]"${arr[$[index+0]]}" update"
				to=${arr[$[index+3]]}

				mail -s "$subject" $to < svn.log

				sed -i '/'$prj'/{s/\(.*#.*#\)[0-9]\+/\1'$rev_new'/}' $conf_file
			fi
		}
		done

		sleep 2
	done

	exit 0


__pmt.conf__

	project01#http://172.168.1.122/repos/dev/project01#18559#usr01@gmail.com
	project02#http://172.168.1.122/repos/dev/project02#18635#usr02@gmail.com

