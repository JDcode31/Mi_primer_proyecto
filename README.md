# Mi_primer_proyecto
import tkinter as tk

# Crear la ventana principal
ventana = tk.Tk()
ventana.title("Calculadora JD Code")
ventana.geometry("300x400")
ventana.resizable(False, False)
ventana.configure(bg="#1e1e1e")

# Variable para mostrar los números y operaciones
expresion = ""

# Función para actualizar el texto
def presionar(valor):
    global expresion
    expresion += str(valor)
    entrada_texto.set(expresion)

# Función para calcular el resultado
def calcular():
    global expresion
    try:
        resultado = str(eval(expresion))
        entrada_texto.set(resultado)
        expresion = resultado
    except:
        entrada_texto.set("Error")
        expresion = ""

# Función para borrar la pantalla
def limpiar():
    global expresion
    expresion = ""
    entrada_texto.set("")

# Campo de entrada
entrada_texto = tk.StringVar()
entrada = tk.Entry(ventana, textvariable=entrada_texto, font=("Arial", 20), bg="#2e2e2e", fg="white", justify="right")
entrada.grid(row=0, column=0, columnspan=4, ipadx=8, ipady=15, padx=10, pady=10)

# Botones de la calculadora
botones = [
    ('7',1,0), ('8',1,1), ('9',1,2), ('/',1,3),
    ('4',2,0), ('5',2,1), ('6',2,2), ('*',2,3),
    ('1',3,0), ('2',3,1), ('3',3,2), ('-',3,3),
    ('0',4,0), ('.',4,1), ('=',4,2), ('+',4,3),
]

for (texto, fila, columna) in botones:
    if texto == "=":
        tk.Button(ventana, text=texto, width=5, height=2, bg="#0078D7", fg="white",
                  font=("Arial", 15), command=calcular).grid(row=fila, column=columna, padx=5, pady=5)
    else:
        tk.Button(ventana, text=texto, width=5, height=2, bg="#333333", fg="white",
                  font=("Arial", 15),
                  command=lambda t=texto: presionar(t)).grid(row=fila, column=columna, padx=5, pady=5)

# Botón de limpiar
tk.Button(ventana, text="C", width=23, height=2, bg="#FF3B30", fg="white",
          font=("Arial", 15), command=limpiar).grid(row=5, column=0, columnspan=4, padx=5, pady=5)

ventana.mainloop()
