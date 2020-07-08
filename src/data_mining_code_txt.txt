import collections

#Read xml file
try:
    file = open("dblp-2020-04-01.xml", encoding="utf8")
except FileNotFoundError:
    print("File not found.")

#Read xml file line by line
years = []
count_lines = 0

while True:
    try:
        line = file.readline()
        count_lines = count_lines + 1
    except NameError:
        print("Data not found.")
    try:
        if not line:
            break;
        if(line[0:6] == "<year>"):
            years.append(line[6:10].strip())
    except NameError:
        print("Years not found.")
        break;

print(f"File's lines: {count_lines} \n")

years_freq = collections.Counter(years)
years_freq = dict(years_freq)

for key,value in sorted(years_freq.items(),reverse=True):
        print(f"{key} {value}")

#Create and write a file with all phdthesis and year from data set
f = open("phdthesis.txt","w")
for key,value in sorted(years_freq.items()):
        f.write(f"{key} {value} \n")
f.close()

#Create and write a file with phdthesis and year from data set till 2010
f = open("phdthesisTill2010.txt","w")
for key,value in sorted(years_freq.items()):
    if(key == "2011"):
        f.close()
        break;
    f.write(f"{key} {value} \n")




