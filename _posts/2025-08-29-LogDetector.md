---
layout: post
title:  "Log Detector"
start_date: 2024-04-16
end_date: 2024-06-08
excerpt: "Log Delay/Reversal/Notcoming/Missing Detector"
project: true
company: "Doople"
tags:
- project
comments: false
---

## LogDetector

.zip,.gz 으로 압축된 Log파일을 가져와서 데이터가 순서대로 들어왔는지, 역전,누락,지연 등의 특이사항이 있는지 확인하고 Report 하는 프로그램

폴더 내 .zip, .gz, .log 파일 전부 판별 가능
내가 원하는 장비,원하는 Plan 만 골라서 판별 가능
내가 원하는 시간대의 Log들만 판별 가능
Log 파일 빠르게 읽고 Abnormal Case 판별 가능
46,400KB Receive.log / 68,543KB Send.log => 판별 1.3s 소요

[[PPT]LogDetectionTool](/assets/pdf/LogDetectionTool.pdf)
