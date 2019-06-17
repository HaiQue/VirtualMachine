import numpy as np

class VM:
    def __init__(a, code, komanda):
        a.code = code
        a.komanda = komanda

mas = []  # komandu masyvas
reg = [0] * 16
file_eof = False
veikia = True

def read_binary(path):
    f = open(path, "rb")
    while True:
        code = f.read(1)
        komanda = f.read(1)

        if code == b"" or komanda == b"":
            break

        vm = VM(int(hex(ord(code)), 16), int(hex(ord(komanda)), 16))
        mas.append(vm)

def calculate(komanda):
    xreg = komanda & 0x0F
    yreg = (komanda & 0xF0) >> 4
    return xreg, yreg

read_binary("decryptor.bin")
data = open("q1_encr.txt", "r")
vieta = 0

while veikia:
    vieta = int(vieta)

    code = mas[vieta].code                 # nusakyta komanda
    komanda = np.int8(mas[vieta].komanda)  # skaicius
    rx, ry = calculate(komanda)            # registrai

    if code == 0x01:
        reg[rx] += 1

    if code == 0x02:
        reg[rx] -= 1

    if code == 0x03:
        reg[rx] = reg[ry]

    if code == 0x04:
        reg[0] += komanda

    if code == 0x05:
        reg[rx] = reg[rx] * 2

    if code == 0x06:
        reg[rx] = reg[rx] / 2

    if code == 0x07:
        vieta += komanda / 2
        continue

    if code == 0x08:
            vieta += komanda / 2
            continue

    if code == 0x09:
            vieta += komanda / 2
            continue

    if code == 0x0A:
        if file_eof == True:
            vieta += komanda / 2
            continue

    if code == 0x0B:
        veikia = False

    if code == 0x0C:
        reg[rx] = reg[rx] + reg[ry]

    if code == 0x0D:
        reg[rx] = reg[rx] - reg[ry]

    if code == 0x0E:
        reg[rx] = reg[rx] ^ reg[ry]

    if code == 0x0F:
        reg[rx] = reg[rx] | reg[ry]

    if code == 0x10:
        c = data.read(1)  # 1s
        if file_eof == False:  # jeigu ne pabaiga
            if c == "":  # jeigu tuscia - baigeme faila
                file_eof = True
            else: reg[rx] = ord(c) #character string of length 1 whose Unicode code point is to be found

    if code == 0x11:
        print(chr(reg[rx]), end="")

    vieta = vieta + 1
