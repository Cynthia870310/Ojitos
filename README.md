from flask import Flask, render_template, request, redirect, url_for

app = Flask(__name__)

# Inventario inicial (podrías conectarlo a una base de datos más adelante)
inventory = [
    {"id": 1, "name": "Teclado", "quantity": 10},
    {"id": 2, "name": "Monitor", "quantity": 5}
]

@app.route('/')
def index():
    return render_template('index.html', inventory=inventory)

@app.route('/add', methods=['POST'])
def add_item():
    name = request.form['name']
    quantity = int(request.form['quantity'])
    new_item = {"id": len(inventory) + 1, "name": name, "quantity": quantity}
    inventory.append(new_item)
    return redirect(url_for('index'))

if __name__ == '__main__':
    app.run(debug=True)
