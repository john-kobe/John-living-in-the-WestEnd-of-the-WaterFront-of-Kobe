# John-living-in-the-WestEnd-of-the-WaterFront-of-Kobe

【シェルスクリプト】

(これを動かしつつ､他のジョブを並行稼働させてマシンの｢負荷｣を見るためのものです)
以下は､Linux環境で"top"コマンドを
タイムスパンに沿って繰り返し､
ジョブの活動状況を処理タイミング毎に､
(金太郎飴を輪切りにするように…)
ファイルに落とし込むスクリプトです｡
某SIer勤務中に請われて作成しました｡
バッククォートは古い書き方ですが(Gemini評です…)､
よろしければ､path､パラメータ等書き換えてお使いください!!
"iotop"コマンドでも応用できます｡
(A.I.に頼めば｢新しい書き方｣に変換してもらえるでしょう…)

#!/bin/bash
# * * * * * * * * *  following codes / written by M.Akai  * * * * * * *
path="/home/john/MyWork/"
prenm="TPEXEC"
extnt=".txt"
cnt=0

`rm -f ${path}${prenm}*`

while :
do
# cnt=`expr ${cnt} + 1`
    if [ ${cnt} -eq 100 ]
    then
      `more ${path}TPEXEC*>${path}TPEXECALL.txt`
      break
    else
      echo ${prenm}${cnt}
      pstnm=`printf %02d ${cnt}`
      `echo>${path}${prenm}${pstnm}${extnt}`
      `LANG=C date +%Y/%m/%d_%H:%M:%S:%3N>>${path}${prenm}${pstnm}${extnt}`
      `echo>>${path}${prenm}${pstnm}${extnt}`
#   `LANG=C top -b -n 1 >${path}${prenm}${pstnm}${extnt}`
      `LANG=C top -b -n 1 >>${path}${prenm}${pstnm}${extnt}`
      `echo>>${path}${prenm}${pstnm}${extnt}`
      cnt=$((cnt+1))
#   usleep 100000
#   sleep 0.5
    fi
done
# * * * * * * * * * * * * * * * *  by M.Akai  * * * * * * * * * * * * *
