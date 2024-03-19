class NodoCola:
    def __init__(self, dato):
        self.dato = dato
        self.siguiente = None

class Cola:
    def __init__(self):
        self.frente = None
        self.final = None

    def encolar(self, dato):
        nuevo_nodo = NodoCola(dato)
        if self.final is None:
            self.frente = nuevo_nodo
        else:
            self.final.siguiente = nuevo_nodo
        self.final = nuevo_nodo

    def desencolar(self):
        if self.frente is None:
            return None
        dato = self.frente.dato
        self.frente = self.frente.siguiente
        if self.frente is None:
            self.final = None
        return dato

    def esta_vacia(self):
        return self.frente is None

class ManejoColasSeguros:
    def __init__(self):
        self.colas = {}

    def llegada_cliente(self, servicio):
        if servicio not in self.colas:
            self.colas[servicio] = Cola()
        self.colas[servicio].encolar(servicio)

    def atender_cliente(self, servicio):
        if servicio in self.colas and not self.colas[servicio].esta_vacia():
            numero_atencion = self.colas[servicio].desencolar()
            return numero_atencion
        else:
            return "No hay clientes en la cola de servicio {}".format(servicio)

# Función principal
def main():
    manejo_colas = ManejoColasSeguros()

    while True:
        accion = input("Ingrese 'C' para la llegada de un cliente o 'A' para atender un cliente: ").upper()

        if accion == 'C':
            numero_servicio = input("Ingrese el número de servicio del cliente: ")
            manejo_colas.llegada_cliente(numero_servicio)
        elif accion == 'A':
            numero_servicio = input("Ingrese el número de servicio que desea atender: ")
            numero_atencion = manejo_colas.atender_cliente(numero_servicio)
            print("Se está atendiendo al cliente con el número de atención:", numero_atencion)
        else:
            print("Entrada no válida. Ingrese 'C' para la llegada de un cliente o 'A' para atender un cliente.")

if __name__ == "__main__":
    main()
