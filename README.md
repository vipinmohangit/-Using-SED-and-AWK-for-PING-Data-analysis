
$ ping -c 4 google.com | awk -F "[= ]" '$2=="bytes"{print ++c "\t" $(NF-1)/1000 }' 1 0.0361 2 0.036 3 0.0357 4 0.0363

Personally, I would do it using grep and only use awk for multiplying the milliseconds by 1000:

$ ping -c4 google.com | grep -Po 'time=\K[\d.]+' | awk '{print NR,$1/1000}' 1 0.0357 2 0.0364 3 0.0364 4 0.0364

$ ping google.com | awk 'BEGIN {FS="[=]|[ ]"} {print $11}' 16.8 16.8 15.7 18.8

PING analysis using AWK I have created a file called ping_analysis.txt which contains the ping data ping 172.217.22.3

Reply from 172.217.22.3 time=41.0 ms Reply from 172.217.22.3 time=40.9 ms Reply from 172.217.22.3 time=42.1 ms Reply from 172.217.22.3 time=41.1 ms Reply from 172.217.22.3 time=42.1 ms Reply from 172.217.22.3 time=41.8 ms

#Default behavior of Awk $ awk '{print}' ping_analysis.txt

#Print the lines which matches with the given pattern $ awk '/41.8/ {print}' ping_analysis.txt

#Splitting lines into fields $ awk '{print$3,$4}' ping_analysis.txt

#Use of NR built-in variables (Display Line Number) $ awk '{print NR,$3,$4}' ping_analysis.txt

#Use of NF built-in variables (Display Last Field) $ awk '{print $4,$NF}' ping_analysis.txt

#Another use of NR built-in variables (Display Line From 2 to 4) $ awk 'NR==2,NR==4 {print NR,$0}' ping_analysis.txt

For ping analysis using SED i have created the file called ping.txt

Reply from 172.217.22.3 time=41.0 ms. Reply from 172.217.22.3 time=40.9 ms Reply from 172.217.22.3 time=42.1 ms Reply from 172.217.22.3 time=41.1 ms Reply from 172.217.22.3 time=42.1 ms. Reply from 172.217.22.3 time=41.8 ms

#Replacing or substituting string $ sed 's/Reply/Response/' ping.txt

#Replacing the nth occurrence of a pattern in a line $ sed 's/Reply/Response/2' ping.txt

#Replacing all the occurrence of the pattern in a line $ sed 's/Reply/Response/g' ping.txt

#Replacing from nth occurrence to all occurrences in a line $ sed 's/Reply/Response/3g' ping.txt

#Replacing string on a specific line number $ sed '3 s/Reply/Response/' ping.txt

#Duplicating the replaced line with /p flag $ sed 's/Reply/Response/p' ping.txt

#Deleting lines from a particular lines $ sed '5d' ping.txt

#Deleting lines from one range to another $ sed '2,4d' ping.txt

#Insert one blank line after each line $ sed G ping.txt

#Insert two blank lines $ sed 'G;G' ping.txt

#View/Print the files( one range to another ) $ sed -n '2,5p' ping_analysis.txt# -Using-SED-and-AWK-for-PING-Data-analysis
