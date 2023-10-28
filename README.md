from PyQt5.QtCore import Qt
from PyQt5.QtWidgets import*
app = QApplication([])
win = QWidget()
from random import shuffle

win.setWindowTitle('Психологический тест')
win.resize(400, 400)

q1 = QLabel('Вы любите шашлык?')
gboxans = QGroupBox('Варианты ответов:')
gboxres = QGroupBox('Результат:')
bttn = QPushButton('Ответить')


a11=QRadioButton('да')
a12=QRadioButton('да')
a13=QRadioButton('да')
a14=QRadioButton('ДА')

res = QLabel('Правильно/Неправильно')
rans = QLabel('текст')

#o1
lh11 = QHBoxLayout()
lh12 = QHBoxLayout()
lh13 = QHBoxLayout()
lv1 = QVBoxLayout()

#o2
lh21 = QHBoxLayout()
lh22 = QHBoxLayout()
lv2 = QVBoxLayout()

#o3
lv3 = QVBoxLayout()

#sborka
#o2
lh21.addWidget(a11)
lh21.addWidget(a12)
lh22.addWidget(a13)
lh22.addWidget(a14)

lv2.addLayout(lh21)
lv2.addLayout(lh22)

gboxans.setLayout(lv2)

#o3
lv3.addWidget(res)
lv3.addWidget(rans)
gboxres.setLayout(lv3)

#o3
lh11.addWidget(q1)
lh12.addWidget(gboxans)
lh12.addWidget(gboxres)
lh13.addWidget(bttn)

#o1
lv1.addLayout(lh11)
lv1.addLayout(lh12)
lv1.addLayout(lh13)

win.setLayout(lv1)

gboxres.hide()

def show_res():
    gboxans.hide()
    gboxres.show()
    bttn.setText('Следующий вопрос')

def show_ans():
    gboxres.hide()
    gboxans.show()
    bttn.setText('Ответить')
    #Сбрасываем все переключатели (СДЕЛАЕМ ПОЗЖЕ)

def analysis_click():
    if bttn.text() == 'Ответить':
        check_ans()

    else:
        ask_que()

class queinf:
    def __init__(self, que, rightanse, wrans1, wrans2, wrans3):
        self.que = que
        self.rightanse = rightanse
        self.wrans1 = wrans1
        self.wrans2 = wrans2
        self.wrans3 = wrans3

list_que = []

qu_qu = queinf ('два плюс два равно', 'титыле', '4','пять', '22')
list_que.append(qu_qu)

qu_qu = queinf ('Меня зовут Мориарти и да,', 'да да да', 'нет. наверное. да я че...','что мам? супчик?', 'я попробовал собственный продукт.')
list_que.append(qu_qu)

qu_qu = queinf ('Queue', 'кью', 'кьюью','куеуе', 'ъ')
list_que.append(qu_qu)

qu_qu = queinf ('у вас есть голоса в голове?', 'нет', 'да','я с ними в города играю', 'помогают списывать')
list_que.append(qu_qu)

list_bttns = [a11, a12, a13, a14]

def ask_que():
    shuffle(list_que)
    question=list_que[0]

    shuffle(list_bttns)
    list_bttns[0].setText(question.rightanse)
    list_bttns[1].setText(question.wrans1)
    list_bttns[2].setText(question.wrans2)
    list_bttns[3].setText(question.wrans3)

    q1.setText(question.que)
    rans.setText(question.rightanse)
    show_ans()


































def check_ans():
    if list_bttns[0].isChecked():
        res.setText('Молодец :3')
        show_res()

    if list_bttns[1].isChecked() or list_bttns[2].isChecked() or list_bttns[3].isChecked():
        res.setText('Будь осторожнее...')
        show_res()       






ask_que()

bttn.clicked.connect(analysis_click)
win.show()
app.exec_()
