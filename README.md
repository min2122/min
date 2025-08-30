
import threading
import webbrowser
from flask import Flask, Response
import tkinter as tk

# ---------- FLASK APP ----------
app = Flask(__name__)

@app.route('/')
def index():
    nombre = "Amor mío"
    mensaje = "Eres la razón por la que sonrío cada día ❤️"

    html_content = f"""
    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <title>💖 Mensaje para mi amor 💖</title>
        <style>
            body {{
                margin: 0;
                padding: 0;
                overflow: hidden;
                font-family: 'Segoe UI', sans-serif;
                background: linear-gradient(to bottom, #ffcccc, #ffe6e6);
                height: 100vh;
                display: flex;
                justify-content: center;
                align-items: center;
                flex-direction: column;
            }}
            h1, p {{
                position: relative;
                z-index: 10;
                text-align: center;
            }}
            h1 {{
                font-size: 3em;
                color: #ff4d4d;
                text-shadow: 2px 2px 8px #fff;
            }}
            p {{
                font-size: 1.5em;
                color: #ff1a1a;
                text-shadow: 1px 1px 6px #fff;
            }}
            .heart {{
                position: absolute;
                width: 30px;
                height: 30px;
                background-color: #ff1a1a;
                transform: rotate(-45deg);
                animation: fall linear infinite;
            }}
            .heart::before,
            .heart::after {{
                content: "";
                position: absolute;
                width: 30px;
                height: 30px;
                background-color: #ff1a1a;
                border-radius: 50%;
            }}
            .heart::before {{ top: -15px; left: 0; }}
            .heart::after {{ left: 15px; top: 0; }}
            @keyframes fall {{
                0% {{ transform: translateY(-100px) rotate(-45deg); opacity: 1; }}
                100% {{ transform: translateY(110vh) rotate(-45deg); opacity: 0; }}
            }}
        </style>
    </head>
    <body>
        <h1>{nombre}</h1>
        <p>{mensaje}</p>

        <script>
            const numHearts = 50;
            for (let i = 0; i < numHearts; i++) {{
                const heart = document.createElement('div');
                heart.classList.add('heart');
                heart.style.left = Math.random() * 100 + 'vw';
                heart.style.animationDuration = (Math.random() * 5 + 5) + 's';
                heart.style.width = heart.style.height = (Math.random() * 20 + 20) + 'px';
                document.body.appendChild(heart);
            }}
        </script>
    </body>
    </html>
    """
    return Response(html_content, mimetype='text/html')

def run_flask():
    app.run(debug=False)

# ---------- TKINTER WINDOW ----------
def open_hearts():
    threading.Thread(target=run_flask).start()
    webbrowser.open("http://127.0.0.1:5000/")

root = tk.Tk()
root.title("Mensaje Romántico 💖")
root.geometry("300x150")
root.resizable(False, False)

label = tk.Label(root, text="¡Hola amor! 💕", font=("Segoe UI", 14))
label.pack(pady=20)

button = tk.Button(root, text="Ver mi sorpresa", font=("Segoe UI", 12), bg="#ff4d4d", fg="white", command=open_hearts)
button.pack(pady=10)

root.mainloop()
