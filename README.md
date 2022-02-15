# 04-script-01-bash

## 1.
Переменная; Значение; Обоснование  
c;	a+b;	переменной присвоилось такое значение поскольку без использования явного обозначения переменных со знаком $ была произведена запись строки  
d;	1+2;	переменные не были обозначены как целочисленные, поэтому в результате получили такую строку  
e;	3;	использован синтаксис арифметический операций, потому получен такой результат  

## 2.

Необходимо:  
-добавить закрывающую скобку в цикле while (())  
-добавить выполнение sleep чтобы между проверками проходил временной промежуток и не так быстро забивался файл логов и место на диске  
-добавить выполнение else break чтобы скрипт завершился  

    while ((1==1))
    do
    curl https://localhost:4757
    if (($? != 0))
    then
    date >> curl.log
    sleep 1
    else
    break
    fi
    done

## 3.

	#!/usr/bin/env bash
	a=192.168.0.1
	b=173.194.222.113
	c=87.250.250.242
	d=80
	declare -i i
	i=1
	while ((i<=5))
	do
	echo -e "\n test no.$i \n" &>> curl.log
	echo -e "\n IP $a \n" &>> curl.log
	curl http://$a:$d --connect-timeout 2 -s -S &>> curl.log
	echo -e "\n IP $b \n" &>> curl.log
	curl http://$b:$d --connect-timeout 2 -s -S &>> curl.log
	echo -e "\n IP $c \n" &>> curl.log
	curl http://$c:$d --connect-timeout 2 -s -S &>> curl.log
	let "i+=1"
	done

## 4.

	#!/usr/bin/env bash
	a=192.168.0.1
	b=173.194.222.113
	c=87.250.250.242
	array_ip=($b $c $a)
	d=80
	while ((1==1))
	do
	for k in ${array_ip[@]}
	do
	curl http://$k:$d --connect-timeout 2 -s -S
	if (($?!=0))
	then
	echo IP $k &>> curl.error
	exit
	fi
	done
	done
