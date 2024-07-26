# from googletrans import Translator, LANGUAGES
# translator = Translator(service_urls=['translate.googleapis.com']) # At direct pip install,this service_url : translate.googleapis.com will not work , this is the indicator that new code had been installed
# translated_text = translator.translate("Salom Dunyo",src="uzbek", dest="english")
# print(translated_text.text)
# languages = list(LANGUAGES.values())
# print(languages)
from tkinter import *
from tkinter.ttk import Combobox
from googletrans import Translator, LANGUAGES

translator = Translator(service_urls=['translate.googleapis.com'])

languages = list(LANGUAGES.values())
tk = Tk()
tk.title("Translator")
tk['bg'] = 'yellow'
tk['padx'] = 10

tillar = []

def clear_text():
    text1.delete(1.0, END)
    text2.delete(1.0, END)


def translate_text():
    translate_from = tanlov1.get()
    translate_to = tanlov2.get()
    
    if translate_to == "Choose language":
        text2.insert(1.0, "Iltimos tarjima qilinadigon tilni tanlang")
        return

    if translate_from == "Auto Detect":
        translate_from = translator.detect(text1)
        translate_from = translate_from.lang

    translation = translator.translate(text1.get(1.0, END), dest=translate_to, src=translate_from)
    text2.insert(1.0, translation.text)


label = Label(bg='yellow', pady=30)
label2 = Label(tk, text="MDRX Translator", bg='yellow', fg="green")
label2.config(font=("Courier", 24))
label.grid(row=0)
label2.place(x=515, y=15)

tanlov1 = Combobox(tk, values=languages, width=20)
tanlov1.set("Auto Detect")
tanlov2 = Combobox(tk, values=languages, width=20)
tanlov2.set("Choose language")

tanlov1.grid(row=1)
Label(bg='yellow').grid(row=2)
Label(bg='yellow').grid(row=2, column=2)
tanlov2.grid(row=1, column=2)

text1 = Text(tk)
text2 = Text(tk)

text1.grid(row=3)
Label(bg='yellow').grid(row=3, column=1)
text2.grid(row=3, column=2)

button1 = Button(tk, text="Translate", bg="light blue", command=translate_text)
button2 = Button(tk, text="Clear", bg="light blue", command=clear_text)
button3 = Button(tk, text="Speech", bg="yellow", fg="white")
button4 = Button(tk, text="Speech", bg="yellow", fg="white")

button1.grid(row=5)
Label(bg='yellow').grid(row=4)
button2.grid(row=5, column=2)
Label(bg='yellow').grid(row=4, column=2)
button3.place(x=540, y=490)
button4.place(x=1190, y=490)



tk.mainloop()
