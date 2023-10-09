import pyautogui
import time
import random
import tkinter as tk
import ctypes

#Convertir en .exe: ejecutar esta fila en cmd en la carpeta (abrir la carpeta y en el cuadro de la ruta escribir cmd)
# pyinstaller --onefile --noconsole --hidden-import pyautogui --hidden-import ctypes --hidden-import random --hidden-import time --hidden-import tkinter ClickIt_v4.py

# Si da error de pyintaller: pip install pyinstaller

# Variable global para el tiempo de espera
Tiempo_Espera = None

# Función para realizar el clic
def click(x, y):
    pyautogui.mouseDown(x, y)
    time.sleep(5)
    pyautogui.mouseUp(x, y)

# Función para cerrar la ventana
def close_window():
    root.destroy()

# Función para actualizar el temporizador
def update_timer():
    current_time = int(label_temporizador["text"])
    if current_time > 0:
        current_time -= 1
        label_temporizador["text"] = str(current_time)
        root.after(1000, update_timer)
    else:
        # Llamar a las funciones después de que el temporizador llegue a cero
        x, y = save_mouse_position()
        click(x, y)
        turn_off_screen()
        lock_session()
        turn_off_screen()

# Función para guardar la posición actual del ratón
def save_mouse_position():
    x, y = pyautogui.position()
    return (x, y)

# Función para bloquear la sesión
def lock_session():
    # Llamada a la función LockWorkStation de la API de Windows para bloquear la sesión
    ctypes.windll.user32.LockWorkStation()

# Función para apagar la pantalla
def turn_off_screen():
    # Llamada a la función SendMessage de la API de Windows para apagar la pantalla
    WM_SYSCOMMAND = 0x0112
    SC_MONITORPOWER = 0xF170
    HWND_BROADCAST = 0xFFFF
    ctypes.windll.user32.SendMessageW(HWND_BROADCAST, WM_SYSCOMMAND, SC_MONITORPOWER, 2)

# Función para iniciar el clic y contar el tiempo
def start_click():
    global Tiempo_Espera
    tiempo = tiempo_espera_entry.get()
    try:
        Tiempo_Espera = int(tiempo)
        if Tiempo_Espera <= 0:
            return
    except ValueError:
        # Manejar el caso en que la entrada no sea un número entero válido
        return

    # Cerrar la ventana de configuración
    root_config.destroy()

    # Mostrar la ventana de cuenta regresiva después de configurar el tiempo
    show_countdown_window()

# Función para mostrar la ventana de cuenta regresiva
def show_countdown_window():
    global root, label_temporizador
    root = tk.Tk()
    root.title("Ejecutando el script")

    label_text = tk.Label(
        root,
        text="El script se está ejecutando, coloque el ratón en la posición correcta.  \n Developed by: Metadona and Wifity",
    )
    label_temporizador = tk.Label(root, text=str(5), font=("Arial", 24))
    label_text.pack(padx=40, pady=40)
    label_temporizador.pack(padx=20, pady=20)

    update_timer()

    root.after(5000, close_window)  # Cerrar la ventana después de 3 segundos (3000 ms)

# Función para crear la ventana de configuración
def create_config_window():
    global root_config, tiempo_espera_entry
    root_config = tk.Tk()
    root_config.title("Configuración del tiempo de espera")

    label_instrucciones = tk.Label(
        root_config,
        text="Introduzca el tiempo de espera (en minutos) y haga clic en 'Aceptar' para continuar:",
    )
    label_instrucciones.pack(padx=20, pady=10)

    tiempo_espera_entry = tk.Entry(root_config)
    tiempo_espera_entry.pack(padx=20, pady=10)

    start_button = tk.Button(root_config, text="Aceptar", command=start_click)
    start_button.pack(padx=20, pady=10)

    root_config.mainloop()

# Llamamos a la función para crear la ventana de configuración
create_config_window()

x, y = save_mouse_position()

click(x, y)

#delta_time = random.randint(0, 60)
#time.sleep(Tiempo_Espera + delta_time)

time.sleep(Tiempo_Espera*60)

click(x, y)

turn_off_screen()
lock_session()
turn_off_screen()
