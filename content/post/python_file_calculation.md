---
title: "Python File Calculation"
date: 2018-09-10T1:20:37+09:00
tags: ['Python', 'os','File']
---

###  Python File Count and File Size ~

変なファイルサイズと数を数えるFunctionです〜

缶GET+1だぜ！

缶GET+1だぜ！
<!--more-->
```
import os

# 罐头的重量(总容量)
tin_Weight = 0
# 种类的数量(文件)
type_Num = 0
# 夹层的数量（文件夹)
mezzanine_Num = 0


# 罐头搜查者
# 缶の追跡者　by ふゆねこ！
def winter_cat_tray(tray_path):
    global tin_Weight
    global type_Num
    global mezzanine_Num
    if len(os.listdir(tray_path)) == 0:
        print('Winter Cat Tins is empty!!!')
    else:
        # 冬喵获得了可能获得了一堆罐头!
        # ふゆねこは多分たくさんの缶を手に入れた！
        for cat_food_tins in os.listdir(tray_path):
            cat_tins_path = os.path.join(tray_path, cat_food_tins)
            # 每个罐头 的具体位置
            # 缶の具体的な位置を示されてる場所
            # print('缶の位置はこちらですよ！:' + cat_tins_path)
            if os.path.isfile(cat_tins_path):
                type_Num = type_Num + 1  # 罐头+1　缶＋１
                tin_Weight = tin_Weight + os.path.getsize(cat_tins_path)
                # 罐头重量　缶の重量
            elif os.path.isdir(cat_tins_path):  # 是罐头并不是罐头里的肉肉(冬喵撬动ing)
                # 　そちらに置いた缶は缶だけだぜ！中身はまだ判明できてない
                mezzanine_Num = mezzanine_Num + 1  # 罐头Get+1!
                # 　缶GET+1だぜ！
                winter_cat_tray(cat_tins_path)  # 撬开Get到的罐头 缶を開いた
    show_all_tins()

def is_tins_clean(tins_path):
    if not os.path.isdir(tins_path):
        print('Error!Tins is dangerous!leaving the computer!')
        return
    winter_cat_tray(tins_path)


# 罐头称重
def str_tins_size_turn(tin):
    k, m, g = 1024, 1024 ** 2, 1024 ** 3
    if tin >= g:
        return str(tin / g) + 'GBytes'
    elif tin >= m:
        return str(tin / m) + 'MBytes'
    elif tin >= k:
        return str(tin / k) + 'KBytes'
    else:
        return str(tin) + 'Bytes'


# 罐头称重 int
def tins_size_turn(tin):
    k, m, g = 1024, 1024 ** 2, 1024 ** 3
    if tin >= g:
        return tin / g
    elif tin >= m:
        return tin / m
    elif tin >= k:
        return tin / k
    else:
        return tin


def show_all_tins():
    if not type_Num == 0:
        print('all tins weight is:' + str_tins_size_turn(tin_Weight))
        print('tin count:%d' % type_Num)
        print('tin location count:', mezzanine_Num)


def get_tins_weight():
    return type_Num


def get_all_tins_weight():
    return tins_size_turn(tin_Weight)
    
```
### End