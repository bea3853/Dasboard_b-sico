import tkinter as tk
from tkinter import *
import matplotlib.pyplot as plt
import pandas as pd 
from tkinter import ttk
from tkinter import messagebox
from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg

def carregar_dados():
    df = pd.read_csv('dados.csv')
    df = df.dropna() # remover valores vazios
    df = df.drop_duplicates() # remove duplicados
    return df
   

def mostrar_estatistica():
    limpar_display()
    
    if dados.empty:
       messagebox.showwarning('Atenção','Não existe dados')
       return
    
    texto = Text(display_frame, wrap=None)
    texto.pack(fill='both',expand = True)


    texto.insert(END, 'ESTATISTICA')
    texto.insert(END, dados.describe(include='all').to_string()) 


def mostra_grafico():
    limpar_display()
    
    if dados.empty:
       messagebox.showwarning('Atenção','Não existe dados')
       return 
    
    fig, ax = plt.subplots(figsize = (8,5))

    if 'Valor' in dados.columns and 'Produtos' in  dados.columns:
        # valor_produto = dados.groupby('Produtos')['Valor'].sum()
        valor_regiao = dados.groupby('Região')['Valor'].sum()
        valor_regiao.plot(kind ='bar', ax=ax, color = 'green')
        ax.set_title('Valor')
        ax.set_ylabel('Valores')
        ax.tick_params(axis = 'x', rotation = 45)
    else:
       messagebox.showerror('Atenção','Erro')


    canvas  =  FigureCanvasTkAgg(fig, master= display_frame)
    canvas.draw()
    canvas.get_tk_widget().pack(fill='both',  expand=True)


def limpar_display():
    for widget in display_frame.winfo_children():
        widget.destroy()


dados = carregar_dados()


# tkinter

root = tk.Tk()
root.title('ANALISE DE DADOS')
root.geometry('800x600')

main_frame = ttk.Frame(root,padding = 10)
main_frame.pack(fill='both', expand=True)

ttk.Label(main_frame, text= 'ANALÍSE', font=('Arial', 16)).pack()

btn_frame = ttk.Frame(main_frame)
btn_frame.pack(pady=10)

ttk.Button(btn_frame, text='Gerar o grafico', command = mostra_grafico).pack(side='left', padx=5)
ttk.Button(btn_frame, text='Gerar estatistica', command = mostrar_estatistica).pack(side='left', padx=5)
ttk.Button(btn_frame, text='Limpar dados', command = limpar_display).pack(side='left', padx=5)

display_frame = ttk.Frame(main_frame)
display_frame.pack(fill='both',expand=True)


root.mainloop()




