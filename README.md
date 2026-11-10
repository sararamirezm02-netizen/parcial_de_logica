productos = { #Diccionario de los productos
    1: ('cafe', 3000, 20),
    2: ('jugo natural', 5000, 15),
    3: ('sandwich', 8000, 10),
    4: ('empanada', 2500, 25),
    5: ('hamburguesa', 12000, 8)
}

#Lista para el pedido
pedido = []

# Funcion para los mostrar el catalogo

def mostrar_productos(productos):
    print (f'{'Codigo' : <8}{'Producto': <15}{'Precio': <10}{'Existencias'}')
    print('-' * 44)
    for codigo, datos in productos.items():
        nombre, precio, existencias = datos
        print(f'{codigo:<8}{nombre:<15}${precio:<9}{existencias}')

def agregar_pedido(pedido, productos, codigo, cantidad):
    nombre, precio, existencias = productos[codigo]
    subtotal = precio * cantidad
    pedido.append((codigo, nombre, cantidad, subtotal))

def registrar_producto(productos, pedido, codigo, cantidad):
    # Validar y registrar un producto er el pedido
    if codigo not in productos:
        print('Producto no encontrado en el sistema')
        return
    
    if cantidad <= 0:
        print('En el momento se encuentra agotado el producto')
        return

    nombre, precio, existencias = productos[codigo]

    if cantidad > existencias:
        print('No contamos con la cantidad de productos')
        return
    
    subtotal = pedido * cantidad
    pedido.append((codigo, nombre, cantidad, subtotal))

    #Las tuplas son inmutables, por eso se crea una nueva con las existencias actualizadas
    productos[codigo] = (nomobre, precio, existencias - cantidad)
    print(f'Se agregaron {cantidad} x {nombre} al pedido')

def leer_entero(mensaje):
    # Leer un entero si el usuario escribe algo invalido retorna None
    try:
        return int(input(mensaje))
    except ValueError:
        return None

def mostrar_resumen(pedido):
    total = calcular_total(pedido)
    if total >= 50000:
        descuento = total * 0.10
    else:
        descuento = 0
    total_final = total - descuento

    print('\n====== RESUMEN DEL PEDIDO ========')
    print(f'{'producto':<18}{'cantidad':<12}{'Subtotal'}')
    print('-' * 41)
    for codigo, nombre, cantidad, subtotal in pedido:
        print(f'{nombre:<18}{cantidad:<12}{subtotal}')
    print('-' * 41)
    print(f'Total : ${total:.0f}')
    print(f'Descuento : ${descuento:.0f}')
    print(f'TOTAL A PAGAR : ${total_final:.0f}')
    print('====================================')

def main():
    while True:
        print("\n========== CAFETERIA ==========")
        print("1. Mostrar productos")
        print("2. Agregar producto al pedido")
        print("3. Finalizar pedido")
        opcion = input("Seleccione una opcion: ")

        if opcion == "1":
            mostrar_productos(productos)
        elif opcion == "2":
            codigo = leer_entero("Codigo del producto: ")
            cantidad = leer_entero("Cantidad: ")
            if codigo is None or cantidad is None:
                print("Cantidad no valida.")
            else:
                registrar_producto(productos, pedido, codigo, cantidad)
        elif opcion == "3":
            if len(pedido) == 0:
                print("No se registraron productos en el pedido.")
            else:
                mostrar_resumen(pedido)
            break
        else:
            print("Opcion no valida.")
    
main()
















































