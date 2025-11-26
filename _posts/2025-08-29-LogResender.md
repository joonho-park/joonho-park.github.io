---
layout: post
title:  "Log Resender"
start_date: 2024-11-29
end_date: 2025-08-19
excerpt: "Log Change Header/Body Resender"
project: true
company: "Doople"
tags:
- project
comments: false
---



## Log Resender

데이터 흐름을 파악하기 위해 기존에 있는 Log 파일을 수정하여 Consumer 로 Send 하는 프로그램 / 장비 시물레이터 
실 장비를 연결하여 대용량, 멀티 환경을 구축하기 어려움에 따라 해당 Resender 를 이용하여
여러 장비에서 한 Consumer 로 데이터를 보내는 환경 구축 가능.
옵션에 따라 설정 가능.
-a Auto Start
-p 로그가 있는 Path
-t Log타입 .gz / .zip
-f 장비정보 세팅 파일을 사용할 지 여부
--fp 장비 정보 세팅 파일의 위치
-u (Required) Consumer URL
-i 각메세지 간 Interval
-c Log파일을 무한정으로 보낼지 여부
-m TRI 를 수정해서 보낼지 여부
-d Debug모드의 여부
-s AsyncSend 할지여부
-l Log를 남길지 여부
--cc Client Count (장비의 대수)
--ct Client Timeout TimeOut 시간
--mt MissingTest  (ex : --mt "1", "3", "5")