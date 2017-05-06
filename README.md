import random

f = True #flag for exit

class Gamer:
    def __init__(self, name, styleFih, sideCoin):
        self.name = name
        self.styleFih = styleFih
        self.sideCoin = sideCoin

def outputTable():
    for i in range(3):
        print(resultTable[i][0], end='')
        for j in range(1, 3):
            print(' | ', resultTable[i][j], end='')
        print('\n------------')

def fillFilds(gamer):
    Style = ''
    Side = ''

    Name = input('Input your name please: ')
    if Name == 'exit':
        return False

    if gamer.styleFih == 'x':
        Style = 'o'
    elif gamer.styleFih == 'o':
        Style = 'x'
    else:
        while Style != 'x' and Style != 'o':
            Style = input('First gamer choose once of char: \'x\' or \'o\' - ')
            if Style == 'exit':
                return False

    if gamer.sideCoin == 'h':
        Side = 't'
    elif gamer.sideCoin == 't':
        Side = 'h'
    else:
        while (Side != 'h' and Side != 't') or gamer.sideCoin == Side:
            Side = input('First gamer choose heads or tails. heads - \'h\', tails - \'t\'. Your are choosing - ')
            if Side == 'exit':
                return False


    return Gamer(Name, Style, Side)

def step(gamer):
    pos = ''
    while True:
        pos = input(gamer.name + ' chose position : ')
        if pos == 'exit':
            return False
        elif len(pos) != 2 or (48 < ord(pos[0]) > 50) or (48 < ord(pos[1]) > 50):
            continue
        elif resultTable[int(pos[0])][int(pos[1])] == '?':
            resultTable[int(pos[0])][int(pos[1])] = gamer.styleFih
            return True
        else:
            print('This place is ful')
            continue

def checkFinish(gamer):
    return ((resultTable[0][0] == resultTable[1][1] == resultTable[2][2] == gamer.styleFih) or
                    (resultTable[0][0] == resultTable[0][1] == resultTable[0][2] == gamer.styleFih) or
                    (resultTable[0][2] == resultTable[1][2] == resultTable[2][2] == gamer.styleFih) or
                    (resultTable[2][2] == resultTable[2][1] == resultTable[2][0] == gamer.styleFih) or
                    (resultTable[2][0] == resultTable[1][0] == resultTable[0][0] == gamer.styleFih) or
                    (resultTable[1][0] == resultTable[1][1] == resultTable[1][2] == gamer.styleFih) or
                    (resultTable[0][1] == resultTable[1][1] == resultTable[2][1] == gamer.styleFih) or
                    (resultTable[0][2] == resultTable[1][1] == resultTable[2][0] == gamer.styleFih))

def simpleWhile(gamer1, gamer2):
    r = random.choice('ht')
    if gamer1.sideCoin == r:
        print(gamer1.name + ' is step first')
        while True:
            print(gamer1.name + ' step :')

            if not step(gamer1):
                print('goodby')
                return False
            elif checkFinish(gamer1):
                print(gamer1.name + ' has won')
                return True

            outputTable()
            print(gamer2.name + ' step :')

            if not step(gamer2):
                print('goodby')
                return False
            elif checkFinish(gamer2):
                print(gamer2.name + ' has won')
                return True
            outputTable()
    else:
        print(gamer2.name + 'is step first')
        while True:
            print(gamer2.name + ' step :')

            if not step(gamer2):
                print('goodby')
                return False
            elif checkFinish(gamer2):
                print(gamer2.name + ' has won')
                return True

            outputTable()
            print(gamer1.name + ' step :')

            if not step(gamer1):
                print('goodby')
                return False
            elif checkFinish(gamer1):
                print(gamer1.name + ' has won')
                return True
            outputTable()

def firstStemOfBot(comp, gamer):

    if (resultTable[1][1] == '?' and
          (resultTable[0][0] == resultTable[2][2] == gamer.styleFih or
           resultTable[0][2] == resultTable[2][0] == gamer.styleFih or
           resultTable[0][1] == resultTable[2][1] == gamer.styleFih or
           resultTable[1][0] == resultTable[1][2] == gamer.styleFih)):
        resultTable[1][1] = comp.styleFih
        return True

    elif (resultTable[0][0] == '?' and
            (resultTable[2][0] == resultTable[1][0] == gamer.styleFih or
             resultTable[2][2] == resultTable[1][1] == gamer.styleFih or
             resultTable[0][1] == resultTable[0][2] == gamer.styleFih)):
        resultTable[0][0] = comp.styleFih
        return True

    elif (resultTable[0][1] == '?' and
            (resultTable[0][0] == resultTable[0][2] == gamer.styleFih or
             resultTable[1][1] == resultTable[2][1] == gamer.styleFih)):
        resultTable[0][1] = comp.styleFih
        return True

    elif (resultTable[0][2] == '?' and
            (resultTable[0][0] == resultTable[0][1] == gamer.styleFih or
             resultTable[1][1] == resultTable[2][0] == gamer.styleFih or
             resultTable[1][2] == resultTable[2][2] == gamer.styleFih)):
        resultTable[0][1] = comp.styleFih
        return True

    elif (resultTable[1][2] == '?' and
            (resultTable[0][2] == resultTable[2][2] == gamer.styleFih or
             resultTable[1][0] == resultTable[1][1] == gamer.styleFih)):
        resultTable[1][2] = comp.styleFih
        return True

    elif (resultTable[2][2] == '?' and
            (resultTable[0][2] == resultTable[1][2] == gamer.styleFih or
             resultTable[1][1] == resultTable[0][0] == gamer.styleFih or
             resultTable[2][1] == resultTable[2][0] == gamer.styleFih)):
        resultTable[2][2] = comp.styleFih
        return True

    elif (resultTable[2][1] == '?' and
            (resultTable[0][1] == resultTable[1][1] == gamer.styleFih or
             resultTable[2][0] == resultTable[2][2] == gamer.styleFih)):
        resultTable[2][1] = comp.styleFih
        return True

    elif (resultTable[2][0] == '?' and
            (resultTable[0][0] == resultTable[1][0] == gamer.styleFih or
             resultTable[2][1] == resultTable[2][2] == gamer.styleFih or
             resultTable[0][2] == resultTable[1][1] == gamer.styleFih)):
        resultTable[2][0] = comp.styleFih
        return True

    elif (resultTable[1][0] == '?' and
            (resultTable[0][0] == resultTable[2][0] == gamer.styleFih or
             resultTable[1][1] == resultTable[1][2] == gamer.styleFih)):
        resultTable[1][0] = comp.styleFih
        return True

def secondStep(comp, gamer):

    if resultTable[1][1] == '?':
        resultTable[1][1] = comp.styleFih
        return True

    elif (resultTable[0][0] == '?' and
            (resultTable[0][1] != gamer.styleFih and resultTable[0][2] != gamer.styleFih) and
            (resultTable[1][0] != gamer.styleFih and resultTable[2][0] != gamer.styleFih)):
        resultTable[0][0] = comp.styleFih
        return True

    elif (resultTable[0][2] == '?' and
            (resultTable[0][0] != gamer.styleFih and resultTable[0][1] != gamer.styleFih) and
            (resultTable[1][2] != gamer.styleFih and resultTable[2][2] != gamer.styleFih)):
        resultTable[0][2] = comp.styleFih
        return True

    elif (resultTable[2][2] == '?' and
            (resultTable[0][2] != gamer.styleFih and resultTable[1][2] != gamer.styleFih) and
            (resultTable[2][0] != gamer.styleFih and resultTable[2][1] != gamer.styleFih)):
        resultTable[2][2] = comp.styleFih
        return True

    elif (resultTable[2][0] == '?' and
            (resultTable[0][0] != gamer.styleFih and resultTable[1][0] != gamer.styleFih) and
            (resultTable[2][1] != gamer.styleFih and resultTable[2][2] != gamer.styleFih)):
        resultTable[2][0] = comp.styleFih
        return True

def thirdStep(comp, gamer):
    if  (resultTable[1][1] == comp.styleFih):

        if (resultTable[0][1] == '?' and
            ((resultTable[0][0] != gamer.styleFih and resultTable[0][2] != gamer.styleFih) or
                resultTable[2][1] != gamer.styleFih)):
            resultTable[0][1] = comp.styleFih

        elif (resultTable[1][2] == '?' and
            ((resultTable[0][2] != gamer.styleFih and resultTable[2][2] != gamer.styleFih) or
            resultTable[2][1] != gamer.styleFih)):
            resultTable[1][2] = comp.styleFih

        elif (resultTable[2][1] == '?' and
                  ((resultTable[2][0] != gamer.styleFih and resultTable[2][2] != gamer.styleFih) or
                   resultTable[0][1] != gamer.styleFih)):
            resultTable[2][1] = comp.styleFih

        elif (resultTable[0][1] == '?' and
                  ((resultTable[0][2] != gamer.styleFih and resultTable[0][0] != gamer.styleFih) or
                   resultTable[1][2] != gamer.styleFih)):
            resultTable[0][1] = comp.styleFih
    else:
        if (resultTable[0][1] == '?' and
                (resultTable[0][0] == comp.styleFih or resultTable[0][2] == comp.styleFih)):
            resultTable[0][1] = comp.styleFih

        elif (resultTable[1][2] == '?' and
                (resultTable[0][2] == comp.styleFih and resultTable[2][2] == comp.styleFih)):
            resultTable[1][2] = comp.styleFih

        elif (resultTable[2][1] == '?' and
                  (resultTable[2][0] == comp.styleFih and resultTable[2][2] == comp.styleFih)):
            resultTable[2][1] = comp.styleFih

        elif (resultTable[0][1] == '?' and
                  (resultTable[0][2] == comp.styleFih and resultTable[0][0] == comp.styleFih)):
            resultTable[0][1] = comp.styleFih

def hardWhile(gamer1, comp):
    r = random.choice('ht')
    if gamer1.sideCoin == r:
        print(gamer1.name + ' is step first')
        while True:
            print(gamer1.name + ' step :')

            if not step(gamer1):
                print('goodby')
                return False
            elif checkFinish(gamer1):
                print(gamer1.name + ' has won')
                return True

            outputTable()
            print('Computer is steping :')

            if firstStemOfBot(comp, comp):
                pass
            elif firstStemOfBot(comp, gamer1):
                pass
            elif secondStep(comp, gamer1):
                pass
            elif thirdStep(comp, gamer1):
                pass

            outputTable()
            if checkFinish(comp):
                print('Computer has won')
                return True
    else:
        print('Computer is step first')
        while True:
            print('Computer is steping :')

            if firstStemOfBot(comp, comp):
                pass
            elif firstStemOfBot(comp, gamer1):
                pass
            elif secondStep(comp, gamer1):
                pass
            elif thirdStep(comp, gamer1):
                pass

            outputTable()
            if checkFinish(comp):
                print('Computer has won')
                return True


            print(gamer1.name + ' step :')

            if not step(gamer1):
                print('goodby')
                return False
            elif checkFinish(gamer1):
                print(gamer1.name + ' has won')
                return True
            outputTable()


# gamer = Gamer('', '', '')
#
# gamer1 = fillFilds(gamer)
# if not gamer1:
#     print('goodby')
# else:
#     print(gamer1.styleFih + '  ' + gamer1.sideCoin)
#
# gamer2 = fillFilds(gamer1)
# if not gamer2:
#     print('goodby')
# else:
#     print(gamer2.styleFih + ' ' + gamer2.sideCoin)



resultTable = [['?', '?', '?'], ['?', '?', '?'], ['?', '?', '?']]

regimeGame = None
while regimeGame != '1' and regimeGame != '2' and regimeGame != 'exit':
    regimeGame = input('Chose regime game \nWith human press number - \'1\'. With computer press - \'2\'.\nInput exit for leave game')

if regimeGame == '1':
    gamer = Gamer('', '', '')

    gamer1 = fillFilds(gamer)
    if not gamer1:
        print('goodby')
    else:
        print(gamer1.name + ' your style of fish - ' + gamer1.styleFih + ', and side of coin - ' + gamer1.sideCoin)

    gamer2 = fillFilds(gamer1)
    if not gamer2:
        print('goodby')
    else:
        print(gamer2.name + ' your style of fish - ' + gamer2.styleFih + ', and side of coin - ' + gamer2.sideCoin)

    if simpleWhile(gamer1, gamer2):
        print('Goodbye thank for game ;)')
    else: print('Bye')
elif regimeGame == '2':
    gamer = Gamer('', '', '')
    gamer1 = fillFilds(gamer)
    if not gamer1:
        print('goodby')
    else:
        print(gamer1.styleFih + '  ' + gamer1.sideCoin)
    comp = Gamer('Comp', 'x' if gamer1.styleFih == 'o' else 'o', 'h' if gamer1.sideCoin == 't' else 't')

    if hardWhile(gamer1, comp):
        print('Goodbye thank for game ;)')
    else:
        print('Bye')





