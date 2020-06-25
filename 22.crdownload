import os
import math
#making tree
tree = []
def combine(nodes):
    pos = 0
    newnode = []
    if len(nodes) > 1:
        nodes.sort()
        nodes[pos].append('0')
        nodes[pos+1].append('1')
        com_1 = (nodes[pos][0] + nodes[pos+1][0])
        com_2 = (nodes[pos][1] + nodes[pos+1][1])
        newnode.append(com_1)
        newnode.append(com_2)
        com_nodes = []
        com_nodes.append(newnode)
        com_nodes = com_nodes + nodes[2:]
        nodes = com_nodes
        tree.append(nodes)
        combine(nodes)
    return tree

#checking input file existance
while True:
    fn = input('Enter File Name(with extension .txt) : ')
    if not os.path.exists(fn.split('.')[0]+'.txt'):
        print('File does not exist.')
        if input('Want to try again...(Y/N) ').lower() == 'y':
            continue
        else:
            exit(0)
    break
#COMPRESSION PROCESS
with open(fn.split('.')[0]+'.txt', 'r') as f:
    st = f.read()
print('\nProcessing...')
ulet = list(set(st))
if len(ulet) == 1:
    l_bin = [[list(ulet)[0], '1']]
else:
    count = []
    #Counting frequency
    for l in ulet:
        count.append(st.count(l))
        count.append(l)
    nodes = []
    #Making tree
    while len(count) > 0:
        nodes.append(count[:2])
        count = count[2:]
    nodes.sort()
    tree.append(nodes)
    newnode = combine(nodes)
    tree.sort(reverse = True)
    chklst = []
    for lvl in tree:
        for node in lvl:
            if node not in chklst:
                chklst.append(node)
            else:
                lvl.remove(node)
    #Generating Codes
    l_bin = []
    if len(ulet) == 1:
        l_code = [ulet[0], '0']
        l_bin.append(l_code*len(st))
    else:
        for l in ulet:
            l_code = ''
            for node in chklst:
                if len(node)>2 and l in node[1]:
                    l_code = l_code + node[2]
            l_code = [l, l_code]
            l_bin.append(l_code)
#forming sentence with generated code
bin_str = ''
for l in st:
    for i in l_bin:
        if l in i:
            bin_str += i[1]
#creating compressed file
if os.path.exists(fn.split('.')[0]+'.bnr'):
    os.remove(fn.split('.')[0]+'.bnr')
with open(fn.split('.')[0]+'.bnr', "ab+") as f:
        f.write(int(bin_str[:], 2).to_bytes(math.ceil(len(bin_str)//8), 'little'))
#creating file to store code table
if os.path.exists(fn.split('.')[0]+'.dat'):
    os.remove(fn.split('.')[0]+'.dat')
with open(fn.split('.')[0]+'.dat', 'a+') as f:
    f.write(str(len(bin_str)) + '\n')
    for i in l_bin:
        x = i[0]+i[1]
        f.write(x+'\n')
print('Compression Successful...')
input('\nEnter any key...')
