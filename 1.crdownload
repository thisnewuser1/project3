import os
#reading file bit by bit
def bits(f):
    b = f.read(1)
    while len(b) > 0:
        if not b:
            break
        b = ord(b)
        for i in range(8):
            yield b & 1
            b >>= 1
        b = f.read(1)

#checking compressed file existance
while True:
    fn = input('Enter File Name(to decompress) : ')
    if not os.path.exists(fn.split('.')[0]+'.bnr') or not os.path.exists(fn.split('.')[0]+'.dat'):
        print('File does not exist or corrupted file.')
        if input('Want to try again...(Y/N) ').lower() == 'y':
            continue
        else:
            exit(0)
    break
print('\nProcessing...')
#reading compressed file bit by bit
with open(fn.split('.')[0]+'.bnr', 'rb') as f:
    bin_str = ''
    for i in bits(f):
        bin_str += str(i)
bin_str = bin_str[::-1]
#reading file containing code table
with open(fn.split('.')[0]+'.dat', 'r') as f:
    x = f.readline()
    l = int(x)
    l_bin = []
    while len(x) > 0:
        x = f.readline()
        if len(x) > 0:
            l_bin.append([x[0], x[1:len(x)-1]])
bin_str = bin_str[len(bin_str)-l:]
#decompressing file with the help of code table
u_str = ''
code = ''
for d in bin_str:
    code += d
    pos = 0
    for l in l_bin:
        if code == l[1]:
            u_str += l_bin[pos][0]
            code =  ''
        pos += 1
if os.path.exists(fn.split('.')[0]+'_decompressed.txt'):
    os.remove(fn.split('.')[0]+'_decompressed.txt')
with open(fn.split('.')[0]+'_decompressed.txt', 'a+') as f:
    f.write(u_str)
print('Decompression Successful...')
input('\nEnter any key...')
